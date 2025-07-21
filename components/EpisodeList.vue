<!-- components/EpisodeList.vue -->
<template>
  <div class="space-y-4">
    <h2 class="text-xl font-bold">Episodes</h2>
    <div
      v-for="episode in episodes"
      :key="episode.id"
      class="flex items-center space-x-4 p-2 hover:bg-gray-100 rounded"
    >
      <img
        :src="episode.poster || '/placeholder.jpg'"
        :alt="episode.title"
        class="w-16 h-16 object-cover rounded"
      />
      <span class="text-lg">{{ episode.title }}</span>
    </div>
  </div>
</template>

<script setup>
defineProps({
  episodes: {
    type: Array,
    default: () => [],
  },
});
</script>