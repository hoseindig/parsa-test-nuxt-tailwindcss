<!-- pages/index.vue -->
<template>
  <div class="min-h-screen bg-gray-100">
    <div v-if="error" class="text-red-500 text-center p-4">
      Failed to load movie data: {{ error }}
    </div>
    <div v-else-if="loading" class="text-center p-4">Loading...</div>
    <div v-else class="container mx-auto p-4 lg:flex lg:space-x-4">
      <!-- Main Content -->
      <div class="lg:w-3/4">
        <h1 class="text-3xl font-bold mb-4">{{ movie.title_en }} ({{ movie.title_fa }})</h1>
        <p class="text-lg mb-4">Year: {{ movie.year }}</p>
        <RatingDisplay :rating="movie.rating || 0" class="mb-4" />
        <VideoPlayer :poster="movie.poster" />
      </div>
      <!-- Sidebar -->
      <div class="lg:w-1/4 mt-4 lg:mt-0">
        <EpisodeList :episodes="movie.episodes || []" />
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import RatingDisplay from '~/components/RatingDisplay.vue';
import VideoPlayer from '~/components/VideoPlayer.vue';
import EpisodeList from '~/components/EpisodeList.vue';

const movie = ref({});
const loading = ref(true);
const error = ref(null);

const fetchMovieData = async () => {
  try {
    const response = await $fetch('https://ylnk.site/test/?action=info&id=2501');
    movie.value = response;
  } catch (err) {
    error.value = err.message;
  } finally {
    loading.value = false;
  }
};

onMounted(fetchMovieData);
</script>

<style scoped>
@media (max-width: 1024px) {
  .container {
    @apply flex-col;
  }
}
</style>