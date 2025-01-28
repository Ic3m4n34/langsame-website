<template>
  <div class="flex items-center justify-center min-h-screen">
    <div class="w-1/2" v-if="progress < 100">
      <h1 class="text-red-600 mb-4 text-center text-lg">Loading website...</h1>
      <div class="w-full bg-gray-200 rounded-full h-8 overflow-hidden">
        <div
          class="bg-red-600 h-8 rounded-full transition-all ease-linear"
          :style="{ width: `${progress}%` }"
        ></div>
      </div>
    </div>

    <div class="w-full" v-show="progress >= 100">
      <div class="flex flex-col items-center space-y-12 px-4 mx-auto">
        <h1 class="text-red-600 text-6xl md:text-7xl font-black text-center leading-tight tracking-tight">
          Deine Website muss nicht langsam sein!
        </h1>
        <p class="text-xl text-center font-medium rounded-lg p-4 text-red-600">
          Jetzt <span class="font-bold bg-red-600 rounded-md px-2 py-1 text-white">kostenlos</span> beraten lassen!
        </p>

        <div style="width:100%;height:100%;overflow:scroll" id="my-cal-inline"></div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const progress = ref(0)
const duration = 10000 // 10 seconds in milliseconds

onMounted(() => {
  const startTime = performance.now()

  const animate = (currentTime) => {
    const elapsed = currentTime - startTime
    progress.value = Math.min((elapsed / duration) * 100, 100)

    if (elapsed < duration) {
      requestAnimationFrame(animate)
    }
  }

  requestAnimationFrame(animate)
})
</script>

<style scoped>
/* Additional styles can be added here */
</style>
