<template>
  <div class="min-height-100vh has-background-light">
    <AirportHero />
    
    <div class="container mt-6 mb-6">
      <div class="columns">
        <div class="column is-half">
          <TripCard @result="handleResult" @loading="handleLoading" />
        </div>
        <div class="column is-half">
          <ResultCard 
            :result="result" 
            :language="language"
            :isLoading="isLoading" 
            :generationTime="generationTime"
          />
        </div>
      </div>
    </div>
    
    <AppFooter />
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import AirportHero from './components/AirportHero.vue'
import TripCard from './components/TripCard.vue'
import ResultCard from './components/ResultCard.vue'
import AppFooter from './components/AppFooter.vue'

const result = ref('')
const language = ref('')
const isLoading = ref(false)
const generationTime = ref(0)
let startTime = 0

const handleResult = (newResult: string, newLanguage: string) => {
  result.value = newResult
  language.value = newLanguage
  generationTime.value = Math.round((Date.now() - startTime) / 1000)
}

const handleLoading = (loading: boolean) => {
  isLoading.value = loading
  if (loading) {
    startTime = Date.now()
  }
}

</script>

<style scoped>
@import './styles/global.css';
</style>
