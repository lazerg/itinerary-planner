<template>
  <div class="card">
    <div class="card-header">
      <p class="card-header-title is-size-5">
        <span class="icon mr-2">
          <i class="fas fa-edit"></i>
        </span>
        Trip Details
      </p>
    </div>
    <div class="card-content">
      <BaseForm @result="handleResult" @loading="handleLoading" />
    </div>
  </div>
</template>

<script setup lang="ts">
import BaseForm from './BaseForm.vue'

const emit = defineEmits<{
  result: [result: string, language: string]
  loading: [loading: boolean]
}>()

const handleResult = (result: string, language: string) => {
  emit('result', result, language)
}

const handleLoading = (loading: boolean) => {
  emit('loading', loading)
}
</script>

<style scoped>
@import '../styles/cards.css';
</style>