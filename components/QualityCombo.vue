<template>
  <div
    class="inline-flex items-center bg-gray-800 text-white px-4 py-3 rounded-md shadow-lg cursor-pointer hover:bg-gray-700 transition-colors"
  >
    <!-- Dropdown arrow -->
    <svg
      class="w-4 h-4 mr-3 text-gray-400"
      fill="none"
      stroke="currentColor"
      viewBox="0 0 24 24"
    >
      <path
        stroke-linecap="round"
        stroke-linejoin="round"
        stroke-width="2"
        d="M19 9l-7 7-7-7"
      ></path>
    </svg>

    <!-- Text content -->
    <span class="text-sm font-medium whitespace-nowrap">
      1080p – webdl کیفیت
    </span>

    <select
      v-model="selectedQuality"
      class="bg-gray-800 text-white text-sm rounded px-2 py-1 border-none outline-none hover:bg-gray-700 transition-colors duration-200"
      @change="changeQuality"
    >
      <option value="1080p">1080p</option>
      <option value="720p">720p</option>
      <option value="480p">480p</option>
      <option value="360p">360p</option>
    </select>
  </div>
</template>

<script setup>
import { ref, computed, onMounted, onUnmounted } from "vue";
// Props with default values
const props = defineProps({
  title: {
    type: String,
    default: "فیلم EL CAMINO",
  },
  videoSource: {
    type: String,
    default: "/path/to/your/video.mp4",
  },
  posterImage: {
    type: String,
    default: "/path/to/poster.jpg",
  },
  quality: {
    type: String,
    default: "1080p",
  },
  autoplay: {
    type: Boolean,
    default: false,
  },
  muted: {
    type: Boolean,
    default: false,
  },
  reportButtonText: {
    type: String,
    default: "اعلام مشکل",
  },
  oldVersionsButtonText: {
    type: String,
    default: "پلیر تلویزیون های قدیمی",
  },
  newVersionsButtonText: {
    type: String,
    default: "پلیر تلویزیون های قدیمی",
  },
  psychologyButtonText: {
    type: String,
    default: "پلیر تلویزیون های سایکولوژیک",
  },
});

const selectedQuality = ref(props.quality);
</script>
