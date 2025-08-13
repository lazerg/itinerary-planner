<template>
  <div class="hero is-primary is-small hero-with-animation">
    <!-- Airport skyline background -->
    <div class="airport-skyline">
      <div class="building building-1"></div>
      <div class="building building-2"></div>
      <div class="building building-3">
        <!-- Company sign on building -->
        <div class="company-sign">
          <div class="sign-line-1">FarkhodMaxTravel</div>
          <div class="sign-line-2">Group</div>
        </div>
      </div>
      <div class="building building-4"></div>
      <div class="building building-5"></div>
      <div class="control-tower">
        <svg width="24" height="32" viewBox="0 0 24 32" fill="none">
          <rect x="8" y="20" width="8" height="12" fill="rgba(255,255,255,0.8)"/>
          <rect x="6" y="15" width="12" height="5" fill="rgba(255,255,255,0.9)"/>
          <rect x="4" y="10" width="16" height="5" fill="rgba(255,255,255,0.7)"/>
          <rect x="10" y="8" width="4" height="2" fill="rgba(255,255,255,0.9)"/>
          <circle cx="12" cy="6" r="3" fill="rgba(255,0,0,0.8)"/>
        </svg>
      </div>
    </div>
    
    <!-- Clouds -->
    <div class="cloud cloud-1">
      <svg width="32" height="20" viewBox="0 0 32 20" fill="none">
        <path d="M8 14C4 14 2 11 3 8C4 6 6 6 8 8C10 3 16 3 18 8C20 6 22 6 23 8C24 11 22 14 18 14H8Z" fill="rgba(255,255,255,0.7)"/>
      </svg>
    </div>
    <div class="cloud cloud-2">
      <svg width="28" height="18" viewBox="0 0 28 18" fill="none">
        <path d="M6 12C3 12 1 10 2 7C3 5 5 5 6 7C8 3 14 3 16 7C17 5 19 5 20 7C21 10 19 12 16 12H6Z" fill="rgba(255,255,255,0.6)"/>
      </svg>
    </div>
    <div class="cloud cloud-3">
      <svg width="30" height="19" viewBox="0 0 30 19" fill="none">
        <path d="M7 13C4 13 2 11 3 8C4 6 6 6 7 8C9 3 15 3 17 8C18 6 20 6 21 8C22 11 20 13 17 13H7Z" fill="rgba(255,255,255,0.8)"/>
      </svg>
    </div>
    
    <!-- Runway lights -->
    <div class="runway-lights">
      <div class="runway-light"></div>
      <div class="runway-light"></div>
      <div class="runway-light"></div>
      <div class="runway-light"></div>
      <div class="runway-light"></div>
    </div>
    
    <!-- Flying plane with destinations -->
    <div class="flying-plane">
      <i class="fas fa-plane"></i>
      <div class="destination-marker marker-1">
        <svg width="20" height="20" viewBox="0 0 20 20" fill="none">
          <rect x="2" y="16" width="16" height="2" fill="rgba(255,215,0,0.9)"/>
          <rect x="4" y="14" width="12" height="2" fill="rgba(255,215,0,0.8)"/>
          <rect x="6" y="6" width="2" height="8" fill="rgba(255,215,0,0.9)"/>
          <rect x="8" y="8" width="4" height="6" fill="rgba(255,215,0,0.9)"/>
          <rect x="12" y="6" width="2" height="8" fill="rgba(255,215,0,0.9)"/>
          <rect x="7" y="2" width="6" height="4" fill="rgba(255,215,0,0.9)"/>
        </svg>
      </div>
      <div class="destination-marker marker-2">
        <svg width="20" height="20" viewBox="0 0 20 20" fill="none">
          <rect x="9" y="2" width="2" height="16" fill="rgba(255,215,0,0.9)"/>
          <rect x="7" y="4" width="6" height="2" fill="rgba(255,215,0,0.8)"/>
          <rect x="6" y="8" width="8" height="2" fill="rgba(255,215,0,0.8)"/>
          <rect x="5" y="12" width="10" height="2" fill="rgba(255,215,0,0.8)"/>
          <rect x="4" y="16" width="12" height="2" fill="rgba(255,215,0,0.9)"/>
        </svg>
      </div>
      <div class="destination-marker marker-3">
        <svg width="20" height="20" viewBox="0 0 20 20" fill="none">
          <rect x="2" y="16" width="16" height="2" fill="rgba(255,215,0,0.9)"/>
          <rect x="4" y="10" width="12" height="6" fill="rgba(255,215,0,0.8)"/>
          <rect x="6" y="6" width="8" height="4" fill="rgba(255,215,0,0.9)"/>
          <rect x="8" y="2" width="4" height="4" fill="rgba(255,215,0,0.9)"/>
          <circle cx="10" cy="4" r="1" fill="rgba(255,0,0,0.8)"/>
        </svg>
      </div>
      <div class="destination-marker marker-4">
        <svg width="20" height="20" viewBox="0 0 20 20" fill="none">
          <rect x="8" y="16" width="4" height="2" fill="rgba(255,215,0,0.9)"/>
          <rect x="9" y="8" width="2" height="8" fill="rgba(255,215,0,0.9)"/>
          <path d="M7 8C7 6 8 4 10 4C12 4 13 6 13 8C13 10 10 12 10 12C10 12 7 10 7 8Z" fill="rgba(0,255,150,0.8)"/>
          <rect x="9" y="2" width="2" height="6" fill="rgba(255,215,0,0.9)"/>
          <path d="M8 2L10 0L12 2H8Z" fill="rgba(255,215,0,0.9)"/>
        </svg>
      </div>
    </div>
    
    <div class="hero-body">
      <div class="container">
        <h1 class="title is-2 has-text-weight-bold has-text-white">
          <span class="icon is-large mr-3">
            <i class="fas fa-map-marked-alt"></i>
          </span>
          Itinerary Planner
        </h1>
        <p class="subtitle is-5 has-text-white-bis">
          Create personalized travel itineraries with AI assistance
        </p>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
// No props or logic needed for this component
</script>

<style scoped>
@import '../styles/hero.css';
</style>