<!-- src/components/BirthdayCake.vue -->

<script setup lang="ts">
import { ref, onMounted } from "vue";

const isVisible = ref(false);
const candlesLit = ref(true);
const showMessage = ref(false);

onMounted(() => {
  setTimeout(() => {
    isVisible.value = true;
  }, 100);

  setTimeout(() => {
    showMessage.value = true;
  }, 1500);
});

const blowCandles = () => {
  candlesLit.value = false;
};
</script>

<template>
  <div
    class="flex flex-col items-center justify-center transition-all duration-1000 scale-[0.6] md:scale-75"
    :class="
      isVisible ? 'opacity-100 scale-[0.6] md:scale-75' : 'opacity-0 scale-50'
    "
  >
    <!-- Birthday Cake Container -->
    <div class="relative" @click="blowCandles">
      <!-- Candle Glow Effect -->
      <div
        v-if="candlesLit"
        class="absolute -top-16 md:-top-20 left-1/2 -translate-x-1/2 w-40 md:w-48 h-24 md:h-32 bg-gradient-radial from-yellow-200/40 via-orange-100/20 to-transparent rounded-full blur-xl animate-pulse"
      ></div>

      <!-- Candles -->
      <div
        class="absolute -top-12 md:-top-16 left-1/2 -translate-x-1/2 flex gap-4 md:gap-6"
      >
        <div v-for="i in 3" :key="i" class="flex flex-col items-center">
          <!-- Flame -->
          <div v-if="candlesLit" class="relative">
            <!-- Outer flame -->
            <div
              class="w-3 h-6 md:w-4 md:h-8 rounded-full animate-flicker animate-glow"
              :style="{
                background:
                  'linear-gradient(to top, #ff6b35 0%, #ff9500 30%, #ffcc00 60%, #fff9c4 100%)',
                animationDelay: `${i * 0.1}s`,
              }"
            ></div>
            <!-- Inner flame -->
            <div
              class="absolute bottom-0 left-1/2 -translate-x-1/2 w-1.5 h-3 md:w-2 md:h-4 rounded-full"
              style="background: linear-gradient(to top, #4fc3f7, #fff9c4)"
            ></div>
          </div>

          <!-- Smoke when blown out -->
          <div
            v-else
            class="w-0.5 h-6 md:w-1 md:h-8 opacity-50"
            style="
              background: linear-gradient(
                to top,
                transparent,
                #9e9e9e,
                transparent
              );
            "
          ></div>

          <!-- Candle stick -->
          <div
            class="w-2 h-8 md:w-3 md:h-10 rounded-t-sm"
            :style="{
              background:
                i === 1
                  ? 'linear-gradient(90deg, #f8bbd9, #f48fb1, #f8bbd9)'
                  : i === 2
                    ? 'linear-gradient(90deg, #b3e5fc, #81d4fa, #b3e5fc)'
                    : 'linear-gradient(90deg, #c8e6c9, #a5d6a7, #c8e6c9)',
            }"
          ></div>
        </div>
      </div>

      <!-- Cake Layers -->
      <div class="flex flex-col items-center">
        <!-- Top decoration (cherry/strawberry) -->
        <div class="relative z-10 -mb-2">
          <div
            class="w-6 h-6 md:w-8 md:h-8 bg-red-500 rounded-full shadow-lg relative"
          >
            <div
              class="absolute top-0.5 left-1.5 md:top-1 md:left-2 w-1.5 h-1.5 md:w-2 md:h-2 bg-white/40 rounded-full"
            ></div>
            <div
              class="absolute -top-1.5 md:-top-2 left-1/2 -translate-x-1/2 w-0.5 h-2 md:w-1 md:h-3 bg-green-600 rounded-full"
            ></div>
            <div
              class="absolute -top-0.5 md:-top-1 left-0.5 md:left-1 w-2 h-1.5 md:w-3 md:h-2 bg-green-500 rounded-full transform -rotate-45"
            ></div>
          </div>
        </div>

        <!-- Top layer (smallest) -->
        <div class="relative">
          <div
            class="w-24 h-12 md:w-32 md:h-16 rounded-lg shadow-lg relative overflow-hidden"
            style="
              background: linear-gradient(
                180deg,
                #fce4ec 0%,
                #f8bbd9 50%,
                #f48fb1 100%
              );
            "
          >
            <!-- Frosting drips -->
            <div
              class="absolute top-0 left-0 w-full h-3 md:h-4 bg-white rounded-b-lg"
            ></div>
            <div
              class="absolute top-2 md:top-3 left-3 md:left-4 w-2 md:w-3 h-3 md:h-4 bg-white rounded-b-full"
            ></div>
            <div
              class="absolute top-2 md:top-3 left-9 md:left-12 w-3 md:w-4 h-4 md:h-6 bg-white rounded-b-full"
            ></div>
            <div
              class="absolute top-2 md:top-3 right-3 md:right-4 w-2 md:w-3 h-3.5 md:h-5 bg-white rounded-b-full"
            ></div>
            <div
              class="absolute top-2 md:top-3 right-9 md:right-12 w-1.5 md:w-2 h-2 md:h-3 bg-white rounded-b-full"
            ></div>

            <!-- Decorations -->
            <div
              class="absolute bottom-1.5 md:bottom-2 left-3 md:left-4 w-1.5 md:w-2 h-1.5 md:h-2 bg-pink-300 rounded-full"
            ></div>
            <div
              class="absolute bottom-2 md:bottom-3 left-7 md:left-10 w-1.5 md:w-2 h-1.5 md:h-2 bg-pink-300 rounded-full"
            ></div>
            <div
              class="absolute bottom-1.5 md:bottom-2 right-3 md:right-4 w-1.5 md:w-2 h-1.5 md:h-2 bg-pink-300 rounded-full"
            ></div>
            <div
              class="absolute bottom-2 md:bottom-3 right-7 md:right-10 w-1.5 md:w-2 h-1.5 md:h-2 bg-pink-300 rounded-full"
            ></div>
          </div>
        </div>

        <!-- Middle layer -->
        <div class="relative -mt-1">
          <div
            class="w-36 h-16 md:w-48 md:h-20 rounded-lg shadow-lg relative overflow-hidden"
            style="
              background: linear-gradient(
                180deg,
                #fff9c4 0%,
                #fff59d 50%,
                #ffee58 100%
              );
            "
          >
            <!-- Frosting drips -->
            <div
              class="absolute top-0 left-0 w-full h-4 md:h-5 rounded-b-lg"
              style="background: linear-gradient(180deg, #fce4ec, #f8bbd9)"
            ></div>
            <div
              class="absolute top-3 md:top-4 left-4 md:left-6 w-3 md:w-4 h-4 md:h-5 rounded-b-full"
              style="background: #f8bbd9"
            ></div>
            <div
              class="absolute top-3 md:top-4 left-12 md:left-16 w-2 md:w-3 h-3 md:h-4 rounded-b-full"
              style="background: #f8bbd9"
            ></div>
            <div
              class="absolute top-3 md:top-4 right-4 md:right-6 w-3 md:w-4 h-4 md:h-6 rounded-b-full"
              style="background: #f8bbd9"
            ></div>
            <div
              class="absolute top-3 md:top-4 right-12 md:right-16 w-2 md:w-3 h-2 md:h-3 rounded-b-full"
              style="background: #f8bbd9"
            ></div>

            <!-- Stripe decoration -->
            <div
              class="absolute bottom-2 md:bottom-3 left-0 w-full h-2 md:h-3 flex justify-around"
            >
              <div class="w-2 h-2 md:w-3 md:h-3 bg-pink-400 rounded-full"></div>
              <div class="w-2 h-2 md:w-3 md:h-3 bg-pink-400 rounded-full"></div>
              <div class="w-2 h-2 md:w-3 md:h-3 bg-pink-400 rounded-full"></div>
              <div class="w-2 h-2 md:w-3 md:h-3 bg-pink-400 rounded-full"></div>
              <div class="w-2 h-2 md:w-3 md:h-3 bg-pink-400 rounded-full"></div>
            </div>
          </div>
        </div>

        <!-- Bottom layer (largest) -->
        <div class="relative -mt-1">
          <div
            class="w-48 h-20 md:w-64 md:h-24 rounded-lg shadow-2xl relative overflow-hidden"
            style="
              background: linear-gradient(
                180deg,
                #f8bbd9 0%,
                #f48fb1 50%,
                #ec407a 100%
              );
            "
          >
            <!-- Frosting drips -->
            <div
              class="absolute top-0 left-0 w-full h-5 md:h-6 rounded-b-lg"
              style="background: linear-gradient(180deg, #fff9c4, #fff59d)"
            ></div>
            <div
              class="absolute top-4 md:top-5 left-6 md:left-8 w-4 md:w-5 h-5 md:h-7 rounded-b-full"
              style="background: #fff59d"
            ></div>
            <div
              class="absolute top-4 md:top-5 left-15 md:left-20 w-3 md:w-4 h-4 md:h-5 rounded-b-full"
              style="background: #fff59d"
            ></div>
            <div
              class="absolute top-4 md:top-5 left-24 md:left-32 w-2 md:w-3 h-3 md:h-4 rounded-b-full"
              style="background: #fff59d"
            ></div>
            <div
              class="absolute top-4 md:top-5 right-6 md:right-8 w-4 md:w-5 h-5 md:h-6 rounded-b-full"
              style="background: #fff59d"
            ></div>
            <div
              class="absolute top-4 md:top-5 right-15 md:right-20 w-3 md:w-4 h-6 md:h-8 rounded-b-full"
              style="background: #fff59d"
            ></div>

            <!-- Bottom decoration -->
            <div
              class="absolute bottom-0 left-0 w-full h-3 md:h-4 bg-gradient-to-t from-pink-700 to-transparent"
            ></div>

            <!-- Sprinkles -->
            <div
              class="absolute bottom-5 md:bottom-6 left-4 md:left-6 w-0.5 h-2 md:w-1 md:h-3 bg-blue-400 rounded-full transform rotate-45"
            ></div>
            <div
              class="absolute bottom-6 md:bottom-8 left-9 md:left-12 w-0.5 h-2 md:w-1 md:h-3 bg-green-400 rounded-full transform -rotate-30"
            ></div>
            <div
              class="absolute bottom-4 md:bottom-5 left-15 md:left-20 w-0.5 h-2 md:w-1 md:h-3 bg-yellow-400 rounded-full transform rotate-15"
            ></div>
            <div
              class="absolute bottom-5 md:bottom-7 right-4 md:right-6 w-0.5 h-2 md:w-1 md:h-3 bg-purple-400 rounded-full transform -rotate-45"
            ></div>
            <div
              class="absolute bottom-4 md:bottom-5 right-10 md:right-14 w-0.5 h-2 md:w-1 md:h-3 bg-red-400 rounded-full transform rotate-30"
            ></div>
            <div
              class="absolute bottom-6 md:bottom-8 right-18 md:right-24 w-0.5 h-2 md:w-1 md:h-3 bg-orange-400 rounded-full"
            ></div>
          </div>
        </div>

        <!-- Cake plate -->
        <div
          class="w-52 h-3 md:w-72 md:h-4 bg-gradient-to-b from-gray-200 to-gray-400 rounded-full shadow-lg -mt-1"
        ></div>
        <div
          class="w-40 h-1.5 md:w-56 md:h-2 bg-gray-500 rounded-full -mt-0.5 opacity-30 blur-sm"
        ></div>
      </div>

      <!-- Click hint -->
      <p
        v-if="candlesLit"
        class="text-pink-400 text-xs md:text-sm mt-3 md:mt-4 animate-pulse text-center"
      >
        ✨ Klik kue untuk tiup lilinnya! ✨
      </p>
      <p
        v-else
        class="text-pink-500 text-base md:text-lg mt-3 md:mt-4 animate-heartbeat text-center"
      >
        🎉 Selamat! Permintaanmu akan terkabul! 🎉
      </p>
    </div>

    <!-- Birthday Message -->
    <Transition
      enter-active-class="transition-all duration-1000 ease-out"
      enter-from-class="opacity-0 translate-y-8"
      enter-to-class="opacity-100 translate-y-0"
    >
      <div v-if="showMessage" class="mt-4 md:mt-6 text-center px-4">
        <h1
          class="text-2xl md:text-4xl lg:text-5xl font-bold text-transparent bg-clip-text bg-gradient-to-r from-pink-500 via-rose-500 to-pink-500 animate-pulse-glow mb-2 md:mb-3"
        >
          <span class="my-4">🎂 Happy Birthday! 🎂</span>
        </h1>
        <p class="text-base md:text-lg lg:text-xl text-pink-600">
          Semoga semua mimpi dan harapanmu tercapai! 💖
        </p>
      </div>
    </Transition>
  </div>
</template>

<style scoped>
.bg-gradient-radial {
  background: radial-gradient(circle, var(--tw-gradient-stops));
}
</style>
