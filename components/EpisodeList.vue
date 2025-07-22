<template>
  <div class="text-white">
    <div class="space-y-4">
      <div
        v-for="episode in episodes"
        :key="episode.id"
        class="rounded-lg p-4 hover:bg-gray-700 transition-colors cursor-pointer"
      >
        <div class="flex items-center space-x-4">
          <!-- Movie Poster -->
          <div class="relative flex-shrink-0 pl-3">
            <img
              :src="episode.poster || '/placeholder.jpg'"
              :alt="episode.title"
              class="w-32 h-24 object-cover rounded-lg"
            />
            <div
              class="absolute top-2 right-2 bg-red-600 text-white text-xs px-1.5 py-0.5 rounded"
            >
              {{ episode.quality || "65" }}
            </div>
          </div>

          <!-- Movie Info -->
          <div class="flex-1 space-y-2">
            <div>
              <h3 class="text-lg font-bold text-white mb-1">
                {{ episode.title }}
              </h3>
              <p class="text-sm text-gray-400">
                {{ episode.subtitle || "اجتماعی، سیاسی، هیجانی" }}
              </p>
            </div>

            <!-- Rating -->
            <div class="flex items-center space-x-2">
              <div class="flex items-center space-x-1">
                <div class="flex space-x-0.5">
                  <svg
                    v-for="star in 1"
                    :key="star"
                    class="w-4 h-4"
                    :class="[
                      star <= Math.floor(episode.rating || 3.5)
                        ? 'fill-yellow-400 text-yellow-400'
                        : star === Math.ceil(episode.rating || 3.5) &&
                          (episode.rating || 3.5) % 1 !== 0
                        ? 'fill-yellow-400 text-yellow-400 opacity-50'
                        : 'text-gray-300',
                    ]"
                    fill="currentColor"
                    viewBox="0 0 20 20"
                  >
                    <path
                      d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z"
                    />
                  </svg>
                </div>
                <span class="text-sm text-yellow-400"
                  >({{ episode.rating || "3.5" }})</span
                >
              </div>
            </div>

            <!-- Year -->
            <div class="text-sm text-white flex items-center space-x-1">
              <!-- <svg class="w-3 h-3" fill="currentColor" viewBox="0 0 20 20">
                <path
                  fill-rule="evenodd"
                  d="M6 2a1 1 0 00-1 1v1H4a2 2 0 00-2 2v10a2 2 0 002 2h12a2 2 0 002-2V6a2 2 0 00-2-2h-1V3a1 1 0 10-2 0v1H7V3a1 1 0 00-1-1zm0 5a1 1 0 000 2h8a1 1 0 100-2H6z"
                  clip-rule="evenodd"
                />
              </svg> -->
              <span>{{ episode.year || "2020" }}</span>
            </div>

            <!-- Metadata Row -->
            <div class="flex items-center space-x-3">
              <!-- Age Rating Badge -->
              <div
                class="flex items-center bg-yellow-500 text-black px-2 py-1 rounded-md text-sm font-bold"
              >
                <div
                  class="w-4 h-4 bg-black rounded-sm flex items-center justify-center text-yellow-500 text-xs font-bold mr-1.5"
                >
                  ⚠
                </div>
                <span>{{ episode.ageRating }}</span>
              </div>

              <!-- Duration/Score Badge -->
              <div
                class="flex items-center bg-red-600 text-white px-2 py-1 rounded-md text-sm font-semibold"
              >
                <svg
                  class="w-4 h-4 mr-1.5"
                  fill="currentColor"
                  viewBox="0 0 20 20"
                >
                  <path
                    fill-rule="evenodd"
                    d="M10 18a8 8 0 100-16 8 8 0 000 16zm1-13a1 1 0 10-2 0v4a1 1 0 00.293.707l2.828 2.829a1 1 0 101.415-1.415L11 9.586V5z"
                    clip-rule="evenodd"
                  />
                </svg>
                <span>{{ episode.duration }}</span>
              </div>

              <!-- IMDB Rating Badge -->
              <div
                class="flex items-center bg-yellow-400 text-black px-2 py-1 rounded-md text-sm font-bold"
              >
                <div
                  class="bg-black text-yellow-400 px-1 py-0.5 rounded text-xs font-bold mr-1.5"
                >
                  IMDb
                </div>
              </div>
              <span>{{ episode.imdbScore }}</span>
            </div>
          </div>
        </div>
      </div>

      <!-- Bottom Navigation -->
      <div class="flex items-center justify-center mt-8 text-gray-400">
        <div
          class="flex items-center space-x-2 cursor-pointer hover:text-white transition-colors"
        >
          <span>←</span>
          <span>مشاهده همه فیلم ها</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
defineProps({
  episodes: {
    type: Array,
    default: () => [
      {
        id: 1,
        title: "EL CAMINO فیلم",
        subtitle: "اجتماعی، سیاسی، هیجانی",
        year: "2020",
        rating: 3.5,
        duration: "4.5 / 10",
        quality: "65",
        ageRating: "65",
        imdbScore: "6.4 / 10",
        comments: "45 / 10",
        poster:
          "https://images.unsplash.com/photo-1489599516215-4af8f43135f2?w=300&h=400&fit=crop",
      },
      {
        id: 2,
        title: "Love Lies Bleeding 2024 فیلم",
        subtitle: "اجتماعی، سیاسی، هیجانی",
        year: "2020",
        rating: 3.5,
        duration: "4.5 / 10",
        quality: "65",
        ageRating: "65",
        imdbScore: "6.4 / 10",
        comments: "45 / 10",
        poster:
          "https://images.unsplash.com/photo-1440404653325-ab127d49abc1?w=300&h=400&fit=crop",
      },
      {
        id: 3,
        title: "متری شیش و نیم",
        subtitle: "اجتماعی، سیاسی، هیجانی",
        year: "2020",
        rating: 3.5,
        duration: "4.5 / 10",
        quality: "65",
        ageRating: "65",
        imdbScore: "6.4 / 10",
        comments: "45 / 10",
        poster:
          "https://images.unsplash.com/photo-1509347528160-9a9e33742cdb?w=300&h=400&fit=crop",
      },
    ],
  },
});
</script>
