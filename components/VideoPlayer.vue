<!-- components/VideoPlayer.vue -->
<template>
  <div class="relative w-full h-96 bg-gray-800 rounded-lg overflow-hidden">
    <img
      :src="poster || '/placeholder.jpg'"
      alt="Video Poster"
      class="w-full h-full object-cover"
    />
    <button
      class="absolute inset-0 m-auto w-16 h-16 bg-white rounded-full flex items-center justify-center opacity-75 hover:opacity-100"
    >
      <svg
        class="w-8 h-8 text-gray-800"
        fill="currentColor"
        viewBox="0 0 24 24"
      >
        <path d="M8 5v14l11-7z" />
      </svg>
    </button>
  </div>
</template>

<script setup>
defineProps({
  poster: {
    type: String,
    default: '',
  },
});
</script>