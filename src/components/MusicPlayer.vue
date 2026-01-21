<script setup lang="ts">
import { ref, onMounted } from 'vue'

const emit = defineEmits<{
  started: []
}>()

const isPlaying = ref(false)
const audioRef = ref<HTMLAudioElement | null>(null)
const showPrompt = ref(true)

const toggleMusic = () => {
  if (audioRef.value) {
    if (isPlaying.value) {
      audioRef.value.pause()
    } else {
      audioRef.value.play()
    }
    isPlaying.value = !isPlaying.value
  }
}

const startMusic = () => {
  showPrompt.value = false
  if (audioRef.value) {
    audioRef.value.play()
    isPlaying.value = true
  }
  emit('started')
}

onMounted(() => {
  if (audioRef.value) {
    audioRef.value.volume = 0.5
    audioRef.value.loop = true
  }
})
</script>

<template>
  <!-- Music Start Prompt (appears first) -->
  <Transition
    leave-active-class="transition-all duration-500"
    leave-to-class="opacity-0 scale-95"
  >
    <div 
      v-if="showPrompt"
      class="fixed inset-0 z-[100] bg-gradient-to-br from-pink-100 via-pink-50 to-rose-100 flex flex-col items-center justify-center"
    >
      <div class="text-center px-6">
        <div class="text-8xl mb-6 animate-heartbeat">💝</div>
        <h1 class="text-3xl md:text-5xl font-bold text-pink-600 mb-4">
          Ada yang spesial untukmu...
        </h1>
        <p class="text-lg text-pink-400 mb-8">
          Nyalakan suara untuk pengalaman terbaik 🎵
        </p>
        <button
          @click="startMusic"
          class="px-8 py-4 bg-gradient-to-r from-pink-500 to-rose-500 text-white text-xl font-bold rounded-full shadow-lg hover:shadow-xl transform hover:scale-105 transition-all duration-300 animate-pulse-glow"
        >
          ✨ Buka Sekarang ✨
        </button>
      </div>
    </div>
  </Transition>

  <!-- Music Control Button (floating) -->
  <button
    v-if="!showPrompt"
    @click="toggleMusic"
    class="fixed bottom-6 right-6 z-50 w-14 h-14 bg-gradient-to-r from-pink-500 to-rose-500 text-white rounded-full shadow-lg hover:shadow-xl transform hover:scale-110 transition-all duration-300 flex items-center justify-center"
    :class="{ 'animate-pulse': isPlaying }"
  >
    <span class="text-2xl">{{ isPlaying ? '🔊' : '🔇' }}</span>
  </button>
  
  <!-- Audio Element -->
  <!-- Using a royalty-free birthday music URL - you can replace this -->
  <audio 
    ref="audioRef"
    preload="auto"
  >
    <!-- Default: Happy Birthday instrumental - replace with your own music file -->
    <source src="https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3" type="audio/mpeg">
    <!-- Add your own music file in public folder and use: -->
    <!-- <source src="/your-music.mp3" type="audio/mpeg"> -->
  </audio>
</template>
