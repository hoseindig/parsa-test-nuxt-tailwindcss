<!-- components/RatingDisplay.vue -->
<template>
  <div class="flex items-center space-x-1">
    <span class="text-lg font-semibold">{{ rating.toFixed(1) }}</span>
    <svg
      v-for="star in 5"
      :key="star"
      class="w-5 h-5"
      :class="star <= Math.round(rating) ? 'text-yellow-400' : 'text-gray-300'"
      fill="currentColor"
      viewBox="0 0 24 24"
    >
      <path
        d="M12 .587l3.668 7.431 8.332 1.209-6.001 5.853 1.416 8.265L12 18.897l-7.415 3.897 1.416-8.265-6.001-5.853 8.332-1.209z"
      />
    </svg>
  </div>
</template>

<script setup>
defineProps({
  rating: {
    type: Number,
    default: 0,
  },
});
</script>