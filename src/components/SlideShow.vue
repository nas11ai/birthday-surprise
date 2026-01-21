<script setup lang="ts">
import { ref, onMounted, computed } from 'vue'

const emit = defineEmits<{
  complete: []
}>()

interface Slide {
  text: string
  subtext?: string
  emoji?: string
}

const slides: Slide[] = [
  { text: "Hai Sayang...", emoji: "💕" },
  { text: "Hari ini adalah hari yang spesial", emoji: "✨" },
  { text: "Karena di hari ini...", emoji: "🌸" },
  { text: "Seseorang yang sangat aku cintai", emoji: "💖" },
  { text: "Lahir ke dunia ini", emoji: "🌟" },
  { text: "Terima kasih sudah hadir", subtext: "dalam hidupku", emoji: "🥰" },
  { text: "Kamu adalah hadiah", subtext: "terindah yang pernah aku terima", emoji: "🎁" },
  { text: "Selamat Ulang Tahun", subtext: "Cintaku 💗", emoji: "🎂" }
]

const currentSlide = ref(0)
const isTyping = ref(true)
const displayedText = ref('')
const showSubtext = ref(false)
const isExiting = ref(false)

const currentSlideData = computed(() => slides[currentSlide.value] ?? slides[0])

const typeText = async (text: string) => {
  displayedText.value = ''
  isTyping.value = true
  showSubtext.value = false
  
  for (let i = 0; i <= text.length; i++) {
    displayedText.value = text.slice(0, i)
    await new Promise(resolve => setTimeout(resolve, 80))
  }
  
  isTyping.value = false
  
  const slideData = currentSlideData.value
  if (slideData?.subtext) {
    await new Promise(resolve => setTimeout(resolve, 300))
    showSubtext.value = true
  }
}

const nextSlide = async () => {
  if (currentSlide.value < slides.length - 1) {
    isExiting.value = true
    await new Promise(resolve => setTimeout(resolve, 500))
    isExiting.value = false
    currentSlide.value++
    const slideData = currentSlideData.value
    if (slideData) {
      await typeText(slideData.text)
    }
    await new Promise(resolve => setTimeout(resolve, 2000))
    nextSlide()
  } else {
    await new Promise(resolve => setTimeout(resolve, 2500))
    isExiting.value = true
    await new Promise(resolve => setTimeout(resolve, 800))
    emit('complete')
  }
}

onMounted(async () => {
  await new Promise(resolve => setTimeout(resolve, 1000))
  const slideData = currentSlideData.value
  if (slideData) {
    await typeText(slideData.text)
  }
  await new Promise(resolve => setTimeout(resolve, 2000))
  nextSlide()
})
</script>

<template>
  <div 
    class="min-h-screen flex flex-col items-center justify-center px-6 transition-all duration-500"
    :class="{ 'opacity-0 scale-95': isExiting }"
  >
    <!-- Emoji -->
    <div 
      class="text-6xl mb-8 animate-float"
      :key="currentSlide + '-emoji'"
    >
      {{ currentSlideData?.emoji ?? '💕' }}
    </div>
    
    <!-- Main Text with Typing Effect -->
    <h1 
      class="text-3xl md:text-5xl lg:text-6xl font-bold text-pink-600 text-center mb-4 min-h-[1.5em]"
      :key="currentSlide + '-text'"
    >
      <span class="inline-block">
        {{ displayedText }}
        <span 
          v-if="isTyping" 
          class="inline-block w-[3px] h-[1em] bg-pink-500 ml-1 animate-pulse"
        ></span>
      </span>
    </h1>
    
    <!-- Subtext -->
    <Transition
      enter-active-class="transition-all duration-700 ease-out"
      enter-from-class="opacity-0 translate-y-4"
      enter-to-class="opacity-100 translate-y-0"
    >
      <p 
        v-if="showSubtext && currentSlideData?.subtext"
        class="text-xl md:text-2xl lg:text-3xl text-pink-400 text-center"
      >
        {{ currentSlideData?.subtext ?? '' }}
      </p>
    </Transition>
    
    <!-- Progress Dots -->
    <div class="flex gap-2 mt-12">
      <div 
        v-for="(_, index) in slides" 
        :key="index"
        class="w-2 h-2 rounded-full transition-all duration-300"
        :class="index === currentSlide ? 'bg-pink-500 w-6' : 'bg-pink-300'"
      ></div>
    </div>
  </div>
</template>
