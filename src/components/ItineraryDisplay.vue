<template>
  <div v-if="parsedData" class="simple-itinerary">
    <div class="content">
      <h2 class="title is-4">{{ parsedData.general_information }}</h2>
      
      <div v-if="parsedData.tips" class="mb-4">
        <h3 class="title is-5">{{ translations.tips }}</h3>
        <p>{{ parsedData.tips }}</p>
      </div>

      <div v-if="parsedData.notes" class="mb-4">
        <h3 class="title is-5">{{ translations.notes }}</h3>
        <p>{{ parsedData.notes }}</p>
      </div>

      <div class="days-section">
        <div v-for="(day, index) in parsedData.days" :key="index" class="day-section mb-5">
          <h3 class="title is-4">{{ translations.day }} {{ index + 1 }}</h3>
          <p class="mb-4">{{ day.general_information }}</p>
          
          <div v-for="(place, placeIndex) in day.places" :key="placeIndex" class="place-section mb-4">
            <h4 class="title is-5">{{ place.name }}</h4>
            
            <div v-if="place.history" class="mb-3">
              <strong>{{ translations.history }}:</strong> {{ place.history }}
            </div>
            
            <div v-if="place.reach" class="mb-3">
              <strong>{{ translations.howToGetThere }}:</strong> {{ place.reach }}
            </div>
            
            <div v-if="place.tips" class="mb-3">
              <strong>{{ translations.tips }}:</strong> {{ place.tips }}
            </div>
            
            <div v-if="place.benefits" class="mb-3">
              <strong>{{ translations.whyVisit }}:</strong> {{ place.benefits }}
            </div>
            
            <hr v-if="placeIndex < day.places.length - 1" class="my-4">
          </div>
        </div>
      </div>
    </div>
  </div>
  
  <div v-else class="has-text-centered py-6">
    <span class="icon is-large has-text-danger">
      <i class="fas fa-exclamation-triangle fa-2x"></i>
    </span>
    <p class="has-text-danger mt-3">Failed to parse the itinerary data. Please try again.</p>
  </div>
</template>

<script setup lang="ts">
import { computed } from 'vue'

interface Place {
  name: string
  history: string
  reach: string
  tips: string
  benefits: string
}

interface Day {
  general_information: string
  places: Place[]
}

interface ItineraryData {
  general_information: string
  tips: string
  notes: string
  days: Day[]
}

const props = defineProps<{
  data: string
  language: string
}>()

const parsedData = computed<ItineraryData | null>(() => {
  try {
    return JSON.parse(props.data)
  } catch (error) {
    console.error('Failed to parse itinerary data:', error)
    return null
  }
})

const translations = computed(() => {
  const lang = props.language || 'en'
  
  const translationMap = {
    en: {
      day: 'Day',
      tips: 'Travel Tips',
      notes: 'Important Notes',
      history: 'History',
      howToGetThere: 'How to get there',
      whyVisit: 'Why visit'
    },
    ru: {
      day: 'День',
      tips: 'Советы для путешествий',
      notes: 'Важные заметки',
      history: 'История',
      howToGetThere: 'Как добраться',
      whyVisit: 'Почему стоит посетить'
    },
    uz: {
      day: 'Kun',
      tips: 'Sayohat maslahatlari',
      notes: 'Muhim eslatmalar',
      history: 'Tarix',
      howToGetThere: 'Qanday borish mumkin',
      whyVisit: 'Nima uchun tashrif buyurish kerak'
    }
  }
  
  return translationMap[lang as keyof typeof translationMap] || translationMap.en
})
</script>

<style scoped>
.simple-itinerary {
  background: white;
  padding: 1.5rem;
  border-radius: 8px;
  border: 1px solid #e0e0e0;
}

.day-section {
  border-left: 4px solid #3273dc;
  padding-left: 1rem;
  margin-bottom: 2rem;
}

.place-section {
  padding-left: 1rem;
}

.content p {
  line-height: 1.6;
  margin-bottom: 1rem;
}

.content strong {
  color: #363636;
}
</style>