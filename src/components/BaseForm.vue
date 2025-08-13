<template>
  <div>
    <form @submit.prevent="submitForm">
      <div class="field">
        <label class="label">Name of Leading Tourist</label>
        <div class="control">
          <input 
            class="input" 
            type="text" 
            v-model="formData.nameOfLeadingTourist"
            placeholder="Enter name"
            required
          />
        </div>
        <p class="help">Primary contact person for this trip</p>
      </div>

      <div class="field">
        <label class="label">Language</label>
        <div class="control">
          <div class="select is-fullwidth">
            <select v-model="formData.language" required>
              <option value="">Select language</option>
              <option value="en">English</option>
              <option value="ru">Russian</option>
              <option value="uz">Uzbek</option>
            </select>
          </div>
        </div>
        <p class="help">Itinerary will be generated in this language</p>
      </div>

      <div class="field">
        <label class="label">Number of Tourists</label>
        <div class="control">
          <div class="select is-fullwidth">
            <select v-model="formData.numberOfTourists" required>
              <option value="">Select number</option>
              <option v-for="num in 10" :key="num" :value="num">{{ num }}</option>
            </select>
          </div>
        </div>
        <p class="help">Total people traveling</p>
      </div>

      <div class="field">
        <label class="label">Type of Tourists</label>
        <div class="control">
          <div class="select is-fullwidth">
            <select v-model="formData.typeOfTourists" required>
              <option value="">Select type</option>
              <option value="family">Family</option>
              <option value="friends">Friends</option>
              <option value="solo">Solo</option>
              <option value="couple">Couple</option>
            </select>
          </div>
        </div>
        <p class="help">Influences activity recommendations</p>
      </div>

      <div class="field">
        <label class="label">Season</label>
        <div class="control">
          <div class="select is-fullwidth">
            <select v-model="formData.season" required>
              <option value="">Select season</option>
              <option value="winter">Winter</option>
              <option value="spring">Spring</option>
              <option value="summer">Summer</option>
              <option value="autumn">Autumn</option>
            </select>
          </div>
        </div>
        <p class="help">Affects weather and available activities</p>
      </div>

      <div class="field">
        <label class="label">City Name</label>
        <div class="control">
          <input 
            class="input" 
            type="text" 
            v-model="formData.cityName"
            placeholder="Enter city name"
            required
          />
        </div>
        <p class="help">Main destination to explore</p>
      </div>

      <div class="field">
        <label class="label">Days</label>
        <div class="control">
          <div class="select is-fullwidth">
            <select v-model="formData.days" required>
              <option value="">Select days</option>
              <option v-for="day in 15" :key="day" :value="day">{{ day }}</option>
            </select>
          </div>
        </div>
        <p class="help">Trip duration</p>
      </div>

      <div class="field">
        <div class="control">
          <button class="button is-primary is-fullwidth" type="submit" :disabled="isSubmitting">
            <span class="icon" v-if="isSubmitting">
              <i class="fas fa-spinner fa-spin"></i>
            </span>
            <span>{{ isSubmitting ? 'Creating...' : 'Submit' }}</span>
          </button>
        </div>
      </div>
    </form>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const emit = defineEmits<{
  result: [result: string, language: string]
  loading: [loading: boolean]
}>()

const formData = ref({
  nameOfLeadingTourist: '',
  language: '',
  numberOfTourists: '',
  typeOfTourists: '',
  season: '',
  cityName: '',
  days: ''
})

const isSubmitting = ref(false)

const submitForm = async () => {
  try {
    isSubmitting.value = true
    emit('loading', true)
    
    const prompt = `You are an itinerary planner. Generate ONLY a valid JSON response without any explanatory text before or after. Here is the tourist data:

- nameOfLeadingTourist: ${formData.value.nameOfLeadingTourist}
- language: ${formData.value.language}
- numberOfTourists: ${formData.value.numberOfTourists}
- typeOfTourists: ${formData.value.typeOfTourists}
- season: ${formData.value.season}
- cityName: ${formData.value.cityName}
- days: ${formData.value.days}

Return ONLY valid JSON in this exact format:

{
  "general_information": "greeting for the leading tourist and general city information",
  "tips": "important tips for visiting this city",
  "notes": "additional helpful information",
  "days": [
    {
      "general_information": "what to do on this day",
      "places": [
        {
          "name": "place name",
          "history": "brief history",
          "reach": "how to get there",
          "tips": "visiting tips",
          "benefits": "what makes this place special"
        }
      ]
    }
  ]
}`

    const response = await fetch('https://api.openai.com/v1/chat/completions', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
        'Authorization': `Bearer ${import.meta.env.VITE_OPENAI_API_KEY}`
      },
      body: JSON.stringify({
        model: 'gpt-4o-mini',
        messages: [
          {
            role: 'user',
            content: prompt
          }
        ],
        max_tokens: 2000,
        temperature: 0.7
      })
    })
    
    if (response.ok) {
      const data = await response.json()
      let result = data.choices[0].message.content
      
      // Extract JSON from the response if it contains extra text
      const jsonMatch = result.match(/\{[\s\S]*\}/)
      if (jsonMatch) {
        result = jsonMatch[0]
      }
      
      // Validate JSON before emitting
      try {
        JSON.parse(result)
        emit('result', result, formData.value.language)
      } catch (parseError) {
        console.error('JSON parse error:', parseError)
        emit('result', `Error: Invalid JSON response from AI. Raw response: ${result}`, formData.value.language)
      }
    } else {
      const errorText = await response.text()
      emit('result', `Error: ${response.status} - ${errorText}`, formData.value.language)
    }
  } catch (error) {
    emit('result', `Error: ${error}`, formData.value.language)
  } finally {
    isSubmitting.value = false
    emit('loading', false)
  }
}
</script>