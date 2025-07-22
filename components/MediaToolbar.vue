<template>
  <div class="inline-flex items-center px-4 py-3 rounded-lg space-x-4">
    <!-- Star rating -->
    <div class="flex items-center space-x-1">
      <div v-for="star in 5" :key="star" class="relative">
        <svg
          class="w-9 h-9"
          :class="star <= rating ? 'text-yellow-400' : 'text-gray-500'"
          fill="currentColor"
          viewBox="0 0 24 24"
        >
          <path
            d="M12 2l3.09 6.26L22 9.27l-5 4.87 1.18 6.88L12 17.77l-6.18 3.25L7 14.14 2 9.27l6.91-1.01L12 2z"
          ></path>
        </svg>
      </div>
    </div>

    <!-- Rating numbers -->
    <div class="text-white font-bold text-lg">4.5/10</div>

    <!-- IMDb logo -->
    <div class="bg-yellow-400 text-black font-bold text-sm px-1 py-1 rounded">
      IMDb
    </div>

    <!-- Bookmark icon -->
    <button
      class="text-gray-400 bg-darkgraybutton hover:text-white transition-colors p-3"
    >
      <svg
        class="w-6 h-6"
        fill="none"
        stroke="currentColor"
        viewBox="0 0 21 21"
      >
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          stroke-width="2"
          d="M5 5a2 2 0 012-2h10a2 2 0 012 2v16l-7-3.5L5 21V5z"
        ></path>
      </svg>
    </button>

    <!-- Share icon -->
    <button
      class="text-gray-400 bg-darkgraybutton hover:text-white transition-colors p-3"
    >
      <svg
        class="w-5 h-5"
        fill="none"
        stroke="currentColor"
        viewBox="0 0 22 22"
      >
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          stroke-width="2"
          d="M8.684 13.342C8.886 12.938 9 12.482 9 12c0-.482-.114-.938-.316-1.342m0 2.684a3 3 0 110-2.684m0 2.684l6.632 3.316m-6.632-6l6.632-3.316m0 0a3 3 0 105.367-2.684 3 3 0 00-5.367 2.684zm0 9.316a3 3 0 105.367 2.684 3 3 0 00-5.367-2.684z"
        ></path>
      </svg>
    </button>
  </div>
</template>
<script setup>
import { ref, onMounted } from "vue";
const rating = ref(2);
</script>
