<script setup lang="ts">
import { ref } from "vue";
import FloatingHearts from "./components/FloatingHearts.vue";
import SlideShow from "./components/SlideShow.vue";
import BirthdayCake from "./components/BirthdayCake.vue";
import Confetti from "./components/Confetti.vue";
import PhotoFrame from "./components/PhotoFrame.vue";
import MusicPlayer from "./components/MusicPlayer.vue";

// ============================================
// 🎀 CUSTOMIZE YOUR BIRTHDAY MESSAGE HERE! 🎀
// ============================================

// Nama pacarmu
const girlfriendName = ref("Qonita");

// URL foto pacarmu (taruh foto di folder public dan tulis nama filenya)
// Contoh: '/foto-pacar.jpg' atau bisa juga URL lengkap
const girlfriendPhoto = ref("/qony.jpg");

// ============================================

const currentPhase = ref<"intro" | "slideshow" | "celebration">("intro");
const showContent = ref(false);

const onMusicStart = () => {
  showContent.value = true;
  currentPhase.value = "slideshow";
};

const onSlideShowComplete = () => {
  currentPhase.value = "celebration";
};
</script>

<template>
  <div
    class="min-h-screen bg-gradient-to-br from-pink-100 via-pink-50 to-rose-100 relative overflow-hidden"
  >
    <!-- Background floating hearts -->
    <FloatingHearts v-if="showContent" />

    <!-- Music Player with intro prompt -->
    <MusicPlayer @started="onMusicStart" />

    <!-- Main Content -->
    <div v-if="showContent" class="relative z-10">
      <!-- Slideshow Phase -->
      <Transition
        leave-active-class="transition-all duration-1000"
        leave-to-class="opacity-0"
      >
        <SlideShow
          v-if="currentPhase === 'slideshow'"
          @complete="onSlideShowComplete"
        />
      </Transition>

      <!-- Celebration Phase -->
      <Transition
        enter-active-class="transition-all duration-1000 ease-out"
        enter-from-class="opacity-0"
        enter-to-class="opacity-100"
      >
        <div
          v-if="currentPhase === 'celebration'"
          class="min-h-screen flex flex-col items-center justify-center py-12 px-4"
        >
          <!-- Confetti Effect -->
          <Confetti />

          <!-- Birthday Cake -->
          <BirthdayCake />

          <!-- Photo Frame -->
          <PhotoFrame :photo-url="girlfriendPhoto" :name="girlfriendName" />

          <!-- Special message -->
          <div
            class="mt-12 text-center max-w-lg px-4 animate-fade-in-up"
            style="animation-delay: 3s"
          >
            <p class="text-lg md:text-xl text-pink-600 leading-relaxed">
              Terima kasih sudah menjadi bagian terindah dalam hidupku. Setiap
              hari bersamamu adalah anugerah bagiku. Aku mencintaimu lebih dari
              yang bisa kuungkapkan dengan kata-kata.
              <span class="text-2xl">💕</span>
            </p>
          </div>

          <!-- Footer -->
          <div class="mt-8 text-pink-400 text-sm">
            Made with 💖 just for you
          </div>
        </div>
      </Transition>
    </div>

    <!-- Sparkle decorations -->
    <div class="fixed top-10 left-10 text-3xl animate-sparkle">✨</div>
    <div
      class="fixed top-20 right-20 text-2xl animate-sparkle"
      style="animation-delay: 0.5s"
    >
      ✨
    </div>
    <div
      class="fixed bottom-20 left-20 text-2xl animate-sparkle"
      style="animation-delay: 1s"
    >
      ✨
    </div>
    <div
      class="fixed bottom-10 right-10 text-3xl animate-sparkle"
      style="animation-delay: 1.5s"
    >
      ✨
    </div>
  </div>
</template>
