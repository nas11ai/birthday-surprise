<script setup lang="ts">
import { ref, onMounted } from "vue";

defineProps<{
  photoUrl?: string;
  name?: string;
}>();

const isVisible = ref(false);

onMounted(() => {
  setTimeout(() => {
    isVisible.value = true;
  }, 2000);
});
</script>

<template>
  <Transition
    enter-active-class="transition-all duration-1000 ease-out"
    enter-from-class="opacity-0 scale-75 rotate-12"
    enter-to-class="opacity-100 scale-100 rotate-0"
  >
    <div v-if="isVisible" class="relative">
      <!-- Decorative hearts around frame -->
      <div
        class="absolute -top-3 -left-3 text-xl md:text-2xl animate-heartbeat"
      >
        💕
      </div>
      <div
        class="absolute -top-3 -right-3 text-xl md:text-2xl animate-heartbeat"
        style="animation-delay: 0.2s"
      >
        💕
      </div>
      <div
        class="absolute -bottom-3 -left-3 text-xl md:text-2xl animate-heartbeat"
        style="animation-delay: 0.4s"
      >
        💕
      </div>
      <div
        class="absolute -bottom-3 -right-3 text-xl md:text-2xl animate-heartbeat"
        style="animation-delay: 0.6s"
      >
        💕
      </div>

      <!-- Photo Frame -->
      <div
        class="relative p-2 md:p-3 bg-gradient-to-br from-pink-300 via-rose-300 to-pink-400 rounded-2xl shadow-2xl animate-pulse-glow"
      >
        <!-- Inner frame -->
        <div class="p-1.5 md:p-2 bg-white rounded-xl">
          <!-- Photo placeholder or actual photo -->
          <div
            v-if="!photoUrl"
            class="w-32 h-44 md:w-48 md:h-64 lg:w-56 lg:h-72 bg-gradient-to-br from-pink-100 to-pink-200 rounded-lg flex flex-col items-center justify-center text-pink-400"
          >
            <span class="text-4xl md:text-6xl mb-2">📷</span>
            <span class="text-xs md:text-sm text-center px-4"
              >Tambahkan foto pacarmu di sini!</span
            >
          </div>
          <img
            v-else
            :src="photoUrl"
            :alt="name || 'My Love'"
            class="w-32 h-44 md:w-48 md:h-64 lg:w-56 lg:h-72 object-cover rounded-lg"
          />
        </div>

        <!-- Ribbon decoration -->
        <div class="absolute -top-1.5 md:-top-2 left-1/2 -translate-x-1/2">
          <div class="relative">
            <div class="w-12 h-5 md:w-16 md:h-6 bg-pink-500 rounded-sm"></div>
            <div
              class="absolute -bottom-1.5 md:-bottom-2 left-0 w-0 h-0 border-l-6 border-r-6 border-t-6 md:border-l-8 md:border-r-8 md:border-t-8 border-l-transparent border-r-transparent border-t-pink-500"
            ></div>
            <div
              class="absolute -bottom-1.5 md:-bottom-2 right-0 w-0 h-0 border-l-6 border-r-6 border-t-6 md:border-l-8 md:border-r-8 md:border-t-8 border-l-transparent border-r-transparent border-t-pink-500"
            ></div>
          </div>
        </div>
      </div>

      <!-- Name tag -->
      <div v-if="name" class="mt-3 md:mt-4 text-center">
        <p
          class="text-xl md:text-2xl lg:text-3xl font-bold text-pink-600 animate-heartbeat"
        >
          {{ name }} 💖
        </p>
      </div>
    </div>
  </Transition>
</template>
