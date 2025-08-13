<template>
  <div class="card">
    <div class="card-header">
      <p class="card-header-title is-size-5">
        <span class="icon mr-2">
          <i class="fas fa-route"></i>
        </span>
        Generated Itinerary
      </p>
    </div>
    <div class="card-content">
      <div v-if="isLoading" class="has-text-centered py-6">
        <div class="is-flex is-justify-content-center mb-4">
          <div class="loader"></div>
        </div>
        <p class="has-text-grey is-size-6">Generating your personalized itinerary...</p>
      </div>
      <div v-else-if="result" class="result-content">
        <div class="generation-time mb-3">
          <span class="tag is-success is-light mb-3">
            <span class="icon is-small">
              <i class="fas fa-clock"></i>
            </span>
            Generated in {{ generationTime }}s
          </span>
          <div class="buttons">
            <button 
              class="button is-info is-small" 
              @click="exportToPDF"
              :disabled="isExporting"
            >
              <span class="icon is-small">
                <i class="fas fa-file-pdf"></i>
              </span>
              <span>{{ isExporting ? 'Exporting...' : 'Export PDF' }}</span>
            </button>
          </div>
        </div>
        <div ref="pdfContent">
          <ItineraryDisplay :data="result" :language="language" />
        </div>
      </div>
      <div v-else class="has-text-centered py-6">
        <span class="icon is-large has-text-grey-light mb-3">
          <i class="fas fa-clipboard-list fa-3x"></i>
        </span>
        <p class="has-text-grey">Fill out the form and submit to generate your itinerary</p>
      </div>
    </div>
    
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import ItineraryDisplay from './ItineraryDisplay.vue'
import jsPDF from 'jspdf'
import html2canvas from 'html2canvas'

defineProps<{
  result: string
  language: string
  isLoading: boolean
  generationTime: number
}>()

const pdfContent = ref<HTMLElement>()
const isExporting = ref(false)


const exportToPDF = async () => {
  if (!pdfContent.value) return

  try {
    isExporting.value = true
    
    // Capture the content as canvas with better quality
    const canvas = await html2canvas(pdfContent.value, {
      scale: 2,
      useCORS: true,
      allowTaint: true,
      backgroundColor: '#ffffff',
      height: pdfContent.value.scrollHeight,
      width: pdfContent.value.scrollWidth
    })
    
    // Create PDF
    const pdf = new jsPDF('p', 'mm', 'a4')
    // const imgData = canvas.toDataURL('image/png')
    
    // Calculate dimensions
    const pdfWidth = pdf.internal.pageSize.getWidth()
    const pdfHeight = pdf.internal.pageSize.getHeight()
    const imgWidth = canvas.width
    const imgHeight = canvas.height
    
    // Scale to fit page width with margins
    const margin = 10
    const availableWidth = pdfWidth - (margin * 2)
    const availableHeight = pdfHeight - (margin * 2)
    const ratio = availableWidth / imgWidth
    const scaledHeight = imgHeight * ratio
    
    // Handle multi-page content
    let yPosition = margin
    let remainingHeight = scaledHeight
    let sourceY = 0
    
    while (remainingHeight > 0) {
      const pageHeight = Math.min(remainingHeight, availableHeight)
      const sourceHeight = pageHeight / ratio
      
      // Add new page if not the first
      if (sourceY > 0) {
        pdf.addPage()
        yPosition = margin
      }
      
      // Create a temporary canvas for this page
      const pageCanvas = document.createElement('canvas')
      pageCanvas.width = imgWidth
      pageCanvas.height = sourceHeight
      const pageCtx = pageCanvas.getContext('2d')
      
      if (pageCtx) {
        pageCtx.drawImage(canvas, 0, sourceY, imgWidth, sourceHeight, 0, 0, imgWidth, sourceHeight)
        const pageImgData = pageCanvas.toDataURL('image/png')
        
        pdf.addImage(pageImgData, 'PNG', margin, yPosition, availableWidth, pageHeight)
      }
      
      sourceY += sourceHeight
      remainingHeight -= pageHeight
    }
    
    // Add header to first page
    pdf.setPage(1)
    pdf.setFontSize(16)
    pdf.setTextColor(40, 40, 40)
    pdf.text('Travel Itinerary - FarkhodMaxTravel Group', pdfWidth / 2, 6, { align: 'center' })
    
    // Add footer to all pages
    // @ts-ignore
    const pageCount = pdf.internal.getNumberOfPages()
    for (let i = 1; i <= pageCount; i++) {
      pdf.setPage(i)
      pdf.setFontSize(10)
      pdf.setTextColor(120, 120, 120)
      pdf.text(`Generated on ${new Date().toLocaleDateString()}`, margin, pdfHeight - 5)
      pdf.text(`Page ${i} of ${pageCount}`, pdfWidth - margin, pdfHeight - 5, { align: 'right' })
    }
    
    // Save the PDF
    const fileName = `Itinerary_${new Date().toISOString().split('T')[0]}.pdf`
    pdf.save(fileName)
    
  } catch (error) {
    console.error('Error exporting PDF:', error)
    alert('Failed to export PDF. Please try again.')
  } finally {
    isExporting.value = false
  }
}

</script>

<style scoped>
@import '../styles/cards.css';
@import '../styles/loading.css';
</style>
