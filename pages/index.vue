<!-- pages/index.vue -->
<template>
  <div class="min-h-screen bg-gray-100">
    <div v-if="error" class="text-red-500 text-center p-4">
      Failed to load movie data: {{ error }}
      <button @click="fetchMovieData" class="mt-2 bg-blue-500 text-white px-4 py-2 rounded">Retry</button>
    </div>
    <div v-else class="container mx-auto p-4 lg:flex lg:space-x-4">
      <!-- Main Content -->
      <div class="lg:w-3/4">
        <div v-if="loading" class="animate-pulse">
          <!-- Skeleton for Movie Information -->
          <div class="h-8 bg-gray-300 rounded w-3/4 mb-4"></div>
          <div class="h-6 bg-gray-300 rounded w-1/2 mb-4"></div>
          <div class="h-5 bg-gray-300 rounded w-1/4 mb-4"></div>
          <!-- Skeleton for Rating -->
          <div class="grid grid-cols-1 sm:grid-cols-3 gap-4 mb-4">
            <div class="h-5 bg-gray-300 rounded"></div>
            <div class="h-5 bg-gray-300 rounded"></div>
            <div class="h-5 bg-gray-300 rounded"></div>
          </div>
          <!-- Skeleton for User Rating -->
          <div class="flex space-x-1 mb-4">
            <div v-for="i in 5" :key="i" class="h-6 w-6 bg-gray-300 rounded"></div>
          </div>
          <!-- Skeleton for Video Player -->
          <div class="h-96 bg-gray-300 rounded relative">
            <div class="absolute inset-0 flex items-center justify-center">
              <div class="h-12 w-12 bg-gray-400 rounded-full"></div>
            </div>
          </div>
        </div>
        <div v-else>
          <h1 class="text-3xl font-bold mb-4">{{ movie.title_en }} ({{ movie.title_fa }})</h1>
          <p class="text-lg mb-4">Year: {{ movie.year }}</p>
          <RatingDisplay :ratings="movie.ratings || {}" :userRating="movie.userRating" class="mb-4" />
          <VideoPlayer :poster="movie.poster" />
        </div>
      </div>
      <!-- Sidebar -->
      <div class="lg:w-1/4 mt-4 lg:mt-0">
        <div v-if="loading" class="animate-pulse space-y-4">
          <!-- Skeleton for Episode List -->
          <div v-for="i in 3" :key="i" class="flex items-center space-x-2">
            <div class="w-16 h-16 bg-gray-300 rounded"></div>
            <div class="h-5 bg-gray-300 rounded w-3/4"></div>
          </div>
        </div>
        <EpisodeList v-else :episodes="movie.episodes || []" />
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
  loading.value = true;
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