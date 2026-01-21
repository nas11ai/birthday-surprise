<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'

interface Particle {
  x: number
  y: number
  size: number
  color: string
  speedX: number
  speedY: number
  rotation: number
  rotationSpeed: number
  shape: 'rect' | 'circle' | 'star'
}

const canvasRef = ref<HTMLCanvasElement | null>(null)
let animationId: number
let particles: Particle[] = []

const colors = [
  '#ff69b4', '#ff1493', '#ffb6c1', '#ffc0cb', // pinks
  '#ff6b6b', '#ffd93d', '#6bcb77', '#4d96ff', // rainbow
  '#c9b1ff', '#f8b4d9', '#ffd700', '#ff9f43'  // pastels & gold
]

const createParticle = (x?: number, y?: number): Particle => {
  const shapes: ('rect' | 'circle' | 'star')[] = ['rect', 'circle', 'star']
  const colorIndex = Math.floor(Math.random() * colors.length)
  const shapeIndex = Math.floor(Math.random() * shapes.length)
  return {
    x: x ?? Math.random() * window.innerWidth,
    y: y ?? -20,
    size: 5 + Math.random() * 10,
    color: colors[colorIndex] as string,
    speedX: (Math.random() - 0.5) * 4,
    speedY: 2 + Math.random() * 4,
    rotation: Math.random() * 360,
    rotationSpeed: (Math.random() - 0.5) * 10,
    shape: shapes[shapeIndex] as 'rect' | 'circle' | 'star'
  }
}

const drawStar = (ctx: CanvasRenderingContext2D, x: number, y: number, size: number) => {
  const spikes = 5
  const outerRadius = size
  const innerRadius = size / 2
  
  ctx.beginPath()
  for (let i = 0; i < spikes * 2; i++) {
    const radius = i % 2 === 0 ? outerRadius : innerRadius
    const angle = (i * Math.PI) / spikes - Math.PI / 2
    const px = x + Math.cos(angle) * radius
    const py = y + Math.sin(angle) * radius
    
    if (i === 0) {
      ctx.moveTo(px, py)
    } else {
      ctx.lineTo(px, py)
    }
  }
  ctx.closePath()
  ctx.fill()
}

const draw = () => {
  const canvas = canvasRef.value
  if (!canvas) return
  
  const ctx = canvas.getContext('2d')
  if (!ctx) return
  
  canvas.width = window.innerWidth
  canvas.height = window.innerHeight
  
  ctx.clearRect(0, 0, canvas.width, canvas.height)
  
  // Add new particles occasionally
  if (Math.random() < 0.3) {
    particles.push(createParticle())
  }
  
  // Update and draw particles
  particles = particles.filter(p => {
    p.x += p.speedX
    p.y += p.speedY
    p.speedY += 0.1 // gravity
    p.rotation += p.rotationSpeed
    
    // Apply some air resistance
    p.speedX *= 0.99
    
    ctx.save()
    ctx.translate(p.x, p.y)
    ctx.rotate((p.rotation * Math.PI) / 180)
    ctx.fillStyle = p.color
    
    if (p.shape === 'rect') {
      ctx.fillRect(-p.size / 2, -p.size / 4, p.size, p.size / 2)
    } else if (p.shape === 'circle') {
      ctx.beginPath()
      ctx.arc(0, 0, p.size / 2, 0, Math.PI * 2)
      ctx.fill()
    } else {
      drawStar(ctx, 0, 0, p.size / 2)
    }
    
    ctx.restore()
    
    return p.y < canvas.height + 50
  })
  
  animationId = requestAnimationFrame(draw)
}

// Burst effect for celebration
const burst = (x: number, y: number, count: number = 50) => {
  for (let i = 0; i < count; i++) {
    const particle = createParticle(x, y)
    particle.speedX = (Math.random() - 0.5) * 15
    particle.speedY = -5 - Math.random() * 10
    particles.push(particle)
  }
}

onMounted(() => {
  draw()
  
  // Initial burst from center
  setTimeout(() => {
    burst(window.innerWidth / 2, window.innerHeight / 2, 80)
  }, 500)
  
  // Periodic bursts
  const interval = setInterval(() => {
    burst(
      Math.random() * window.innerWidth,
      Math.random() * window.innerHeight * 0.5,
      30
    )
  }, 3000)
  
  onUnmounted(() => {
    cancelAnimationFrame(animationId)
    clearInterval(interval)
  })
})
</script>

<template>
  <canvas 
    ref="canvasRef" 
    class="fixed inset-0 pointer-events-none z-50"
  ></canvas>
</template>
