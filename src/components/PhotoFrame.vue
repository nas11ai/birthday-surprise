<script setup lang="ts">
import { ref, onMounted } from 'vue'

defineProps<{
  photoUrl?: string
  name?: string
}>()

const isVisible = ref(false)

onMounted(() => {
  setTimeout(() => {
    isVisible.value = true
  }, 2000)
})
</script>

<template>
  <Transition
    enter-active-class="transition-all duration-1000 ease-out"
    enter-from-class="opacity-0 scale-75 rotate-12"
    enter-to-class="opacity-100 scale-100 rotate-0"
  >
    <div 
      v-if="isVisible"
      class="relative mt-8"
    >
      <!-- Decorative hearts around frame -->
      <div class="absolute -top-4 -left-4 text-2xl animate-heartbeat">💕</div>
      <div class="absolute -top-4 -right-4 text-2xl animate-heartbeat" style="animation-delay: 0.2s">💕</div>
      <div class="absolute -bottom-4 -left-4 text-2xl animate-heartbeat" style="animation-delay: 0.4s">💕</div>
      <div class="absolute -bottom-4 -right-4 text-2xl animate-heartbeat" style="animation-delay: 0.6s">💕</div>
      
      <!-- Photo Frame -->
      <div class="relative p-3 bg-gradient-to-br from-pink-300 via-rose-300 to-pink-400 rounded-2xl shadow-2xl animate-pulse-glow">
        <!-- Inner frame -->
        <div class="p-2 bg-white rounded-xl">
          <!-- Photo placeholder or actual photo -->
          <div 
            v-if="!photoUrl"
            class="w-48 h-64 md:w-64 md:h-80 bg-gradient-to-br from-pink-100 to-pink-200 rounded-lg flex flex-col items-center justify-center text-pink-400"
          >
            <span class="text-6xl mb-2">📷</span>
            <span class="text-sm text-center px-4">Tambahkan foto pacarmu di sini!</span>
          </div>
          <img 
            v-else
            :src="photoUrl" 
            :alt="name || 'My Love'"
            class="w-48 h-64 md:w-64 md:h-80 object-cover rounded-lg"
          />
        </div>
        
        <!-- Ribbon decoration -->
        <div class="absolute -top-2 left-1/2 -translate-x-1/2">
          <div class="relative">
            <div class="w-16 h-6 bg-pink-500 rounded-sm"></div>
            <div class="absolute -bottom-2 left-0 w-0 h-0 border-l-8 border-r-8 border-t-8 border-l-transparent border-r-transparent border-t-pink-500"></div>
            <div class="absolute -bottom-2 right-0 w-0 h-0 border-l-8 border-r-8 border-t-8 border-l-transparent border-r-transparent border-t-pink-500"></div>
          </div>
        </div>
      </div>
      
      <!-- Name tag -->
      <div 
        v-if="name"
        class="mt-4 text-center"
      >
        <p class="text-2xl md:text-3xl font-bold text-pink-600 animate-heartbeat">
          {{ name }} 💖
        </p>
      </div>
    </div>
  </Transition>
</template>
