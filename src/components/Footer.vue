<script setup>
import { onMounted, onUnmounted, ref } from 'vue'

// Busuanzi counter setup
onMounted(() => {
  // Load Busuanzi script
  const script = document.createElement('script')
  script.async = true
  script.src = '//busuanzi.ibruce.info/busuanzi/2.3/busuanzi.pure.mini.js'
  document.head.appendChild(script)

  // Handle script load error
  script.onerror = () => {
    console.error('Failed to load Busuanzi counter')

    // Get the containers
    const uvContainer = document.getElementById('busuanzi_container_site_uv')
    const pvContainer = document.getElementById('busuanzi_container_site_pv')

    // Show the containers with fallback values
    if (uvContainer) {
      uvContainer.style.display = 'inline'
      const uvValue = document.getElementById('busuanzi_value_site_uv')
      if (uvValue)
        uvValue.textContent = '--'
    }

    if (pvContainer) {
      pvContainer.style.display = 'inline'
      const pvValue = document.getElementById('busuanzi_value_site_pv')
      if (pvValue)
        pvValue.textContent = '--'
    }
  }
})

// Website runtime calculation
const runtimeDisplay = ref('')
let timerInterval = null

// Set your website's launch date here (YYYY, MM-1, DD, HH, MM, SS)
// Note: Month is 0-indexed (0 = January, 11 = December)
const launchDate = new Date(2025, 3, 2, 0, 0, 0) // April 2, 2025

function updateRuntime() {
  const now = new Date()
  const diff = now - launchDate

  // Calculate time units
  const days = Math.floor(diff / (1000 * 60 * 60 * 24))
  const hours = Math.floor((diff % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60))
  const minutes = Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60))
  const seconds = Math.floor((diff % (1000 * 60)) / 1000)

  // Format the runtime display
  runtimeDisplay.value = `${days}d ${hours}h ${minutes}m ${seconds}s`
}

onMounted(() => {
  // Initial update
  updateRuntime()

  // Update every second
  timerInterval = setInterval(updateRuntime, 1000)
})

onUnmounted(() => {
  // Clean up the interval when component is unmounted
  if (timerInterval) {
    clearInterval(timerInterval)
  }
})
</script>

<template>
  <div class="mt-10 mb-6 prose m-auto flex flex-col slide-enter animate-delay-1200!">
    <div class="flex w-full">
      <span class="text-sm op50"><a target="_blank" href="https://creativecommons.org/licenses/by-nc-sa/4.0/" style="color:inherit">CC BY-NC-SA 4.0</a> 2025-PRESENT © Steven Chen</span>
      <div class="flex-auto" />
    </div>
    <div class="flex w-full mt-2">
      <span class="text-sm op50">
        <span id="busuanzi_container_site_uv" style="display:none">
          Visitors: <span id="busuanzi_value_site_uv" />
        </span>
        <span class="mx-2">|</span>
        <span id="busuanzi_container_site_pv" style="display:none">
          Page Views: <span id="busuanzi_value_site_pv" />
        </span>
        <span class="mx-2">|</span>
        <span>
          Site Age 🚀: <span>{{ runtimeDisplay }}</span>
        </span>
      </span>
    </div>
  </div>
</template>
