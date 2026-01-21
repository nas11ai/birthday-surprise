<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'

interface Heart {
  id: number
  x: number
  y: number
  size: number
  opacity: number
  speed: number
  rotation: number
  rotationSpeed: number
}

const hearts = ref<Heart[]>([])
let animationId: number
let heartId = 0

const createHeart = (): Heart => {
  return {
    id: heartId++,
    x: Math.random() * 100,
    y: 100 + Math.random() * 20,
    size: 10 + Math.random() * 20,
    opacity: 0.3 + Math.random() * 0.5,
    speed: 0.5 + Math.random() * 1,
    rotation: Math.random() * 360,
    rotationSpeed: (Math.random() - 0.5) * 2
  }
}

const animate = () => {
  hearts.value = hearts.value
    .map(heart => ({
      ...heart,
      y: heart.y - heart.speed,
      rotation: heart.rotation + heart.rotationSpeed,
      x: heart.x + Math.sin(heart.y / 30) * 0.3
    }))
    .filter(heart => heart.y > -10)

  if (Math.random() < 0.05) {
    hearts.value.push(createHeart())
  }

  animationId = requestAnimationFrame(animate)
}

onMounted(() => {
  for (let i = 0; i < 15; i++) {
    const heart = createHeart()
    heart.y = Math.random() * 100
    hearts.value.push(heart)
  }
  animate()
})

onUnmounted(() => {
  cancelAnimationFrame(animationId)
})
</script>

<template>
  <div class="fixed inset-0 pointer-events-none overflow-hidden z-0">
    <div
      v-for="heart in hearts"
      :key="heart.id"
      class="absolute text-pink-400"
      :style="{
        left: `${heart.x}%`,
        top: `${heart.y}%`,
        fontSize: `${heart.size}px`,
        opacity: heart.opacity,
        transform: `rotate(${heart.rotation}deg)`,
        transition: 'none'
      }"
    >
      ❤️
    </div>
  </div>
</template>
