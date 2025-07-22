<template>
  <div class="w-full px-3 bg-darkgray rounded-lg overflow-hidden">
    <!-- <VideoTitle /> -->
    <!-- Video Container -->
    <div class="relative group">
      <!-- Video Element -->
      <video
        ref="videoElement"
        class="w-full h-auto"
        :poster="posterImage"
        @loadedmetadata="onLoadedMetadata"
        @timeupdate="onTimeUpdate"
        @click="togglePlay"
      >
        <source :src="videoSource" type="video/mp4" />
        مرورگر شما از پخش ویدیو پشتیبانی نمی‌کند
      </video>

      <!-- Dark Overlay for dramatic effect -->
      <div
        class="absolute inset-0 bg-gradient-to-t from-black/60 via-transparent to-black/20 pointer-events-none"
      ></div>

      <!-- Play/Pause Button (Center) -->
      <div
        v-if="showCenterButton"
        class="absolute inset-0 flex items-center justify-center opacity-0 group-hover:opacity-100 transition-opacity duration-300"
      >
        <button
          @click="togglePlay"
          class="bg-white/20 hover:bg-white/30 rounded-full p-4 backdrop-blur-sm transition-all duration-300 transform hover:scale-110"
        >
          <svg
            v-if="!isPlaying"
            class="w-8 h-8 text-white"
            fill="currentColor"
            viewBox="0 0 24 24"
          >
            <path d="M8 5v14l11-7z" />
          </svg>
          <svg
            v-else
            class="w-8 h-8 text-white"
            fill="currentColor"
            viewBox="0 0 24 24"
          >
            <path d="M6 19h4V5H6v14zm8-14v14h4V5h-4z" />
          </svg>
        </button>
      </div>
    </div>

    <!-- Controls Bar -->
    <div class="bg-gradient-to-r from-gray-900 to-black p-4">
      <!-- Progress Bar -->
      <div class="mb-3">
        <div
          class="w-full bg-gray-700 rounded-full h-1 cursor-pointer"
          @click="seek"
          ref="progressBar"
        >
          <div
            class="bg-red-600 h-1 rounded-full transition-all duration-150"
            :style="{ width: progressPercentage + '%' }"
          ></div>
        </div>
      </div>

      <!-- Controls Row -->
      <div class="flex items-center justify-between text-white">
        <!-- Left Controls -->
        <div class="flex items-center space-x-4">
          <!-- Play/Pause -->
          <button
            @click="togglePlay"
            class="hover:text-red-500 transition-colors duration-200"
          >
            <svg
              v-if="!isPlaying"
              class="w-5 h-5"
              fill="currentColor"
              viewBox="0 0 24 24"
            >
              <path d="M8 5v14l11-7z" />
            </svg>
            <svg v-else class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24">
              <path d="M6 19h4V5H6v14zm8-14v14h4V5h-4z" />
            </svg>
          </button>

          <!-- Skip Forward -->
          <button
            @click="skipForward"
            class="hover:text-red-500 transition-colors duration-200"
          >
            <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24">
              <path d="M4 18l8.5-6L4 6v12zm9-12v12l8.5-6L13 6z" />
            </svg>
          </button>

          <!-- Volume -->
          <div class="flex items-center space-x-2">
            <button
              @click="toggleMute"
              class="hover:text-red-500 transition-colors duration-200"
            >
              <svg
                v-if="!isMuted && volume > 0.5"
                class="w-5 h-5"
                fill="currentColor"
                viewBox="0 0 24 24"
              >
                <path
                  d="M3 9v6h4l5 5V4L7 9H3zm13.5 3c0-1.77-1.02-3.29-2.5-4.03v8.05c1.48-.73 2.5-2.25 2.5-4.02zM14 3.23v2.06c2.89.86 5 3.54 5 6.71s-2.11 5.85-5 6.71v2.06c4.01-.91 7-4.49 7-8.77s-2.99-7.86-7-8.77z"
                />
              </svg>
              <svg
                v-else-if="!isMuted && volume > 0"
                class="w-5 h-5"
                fill="currentColor"
                viewBox="0 0 24 24"
              >
                <path
                  d="M18.5 12c0-1.77-1.02-3.29-2.5-4.03v8.05c1.48-.73 2.5-2.25 2.5-4.02zM5 9v6h4l5 5V4L9 9H5z"
                />
              </svg>
              <svg
                v-else
                class="w-5 h-5"
                fill="currentColor"
                viewBox="0 0 24 24"
              >
                <path
                  d="M16.5 12c0-1.77-1.02-3.29-2.5-4.03v2.21l2.45 2.45c.03-.2.05-.41.05-.63zm2.5 0c0 .94-.2 1.82-.54 2.64l1.51 1.51C20.63 14.91 21 13.5 21 12c0-4.28-2.99-7.86-7-8.77v2.06c2.89.86 5 3.54 5 6.71zM4.27 3L3 4.27 7.73 9H3v6h4l5 5v-6.73l4.25 4.25c-.67.52-1.42.93-2.25 1.18v2.06c1.38-.31 2.63-.95 3.69-1.81L19.73 21 21 19.73l-9-9L4.27 3zM12 4L9.91 6.09 12 8.18V4z"
                />
              </svg>
            </button>

            <input
              v-model="volume"
              type="range"
              min="0"
              max="1"
              step="0.1"
              class="w-20 h-1 bg-gray-700 rounded-lg appearance-none cursor-pointer slider"
              @input="updateVolume"
            />
          </div>

          <!-- Time Display -->
          <div class="text-sm text-gray-300">
            {{ formatTime(currentTime) }} / {{ formatTime(duration) }}
          </div>
        </div>

        <!-- Right Controls -->
        <div class="flex items-center space-x-4">
          <!-- Quality Selector -->
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

          <!-- Fullscreen -->
          <button
            @click="toggleFullscreen"
            class="hover:text-red-500 transition-colors duration-200"
          >
            <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24">
              <path
                d="M7 14H5v5h5v-2H7v-3zm-2-4h2V7h3V5H5v5zm12 7h-3v2h5v-5h-2v3zM14 5v2h3v3h2V5h-5z"
              />
            </svg>
          </button>
        </div>
      </div>
    </div>

    <!-- Bottom Action Buttons (like in the image) -->
    <VideoPlayerActionButton />
  </div>
</template>

<script setup>
import { ref, computed, onMounted, onUnmounted } from "vue";
import VideoTitle from "~/components/VideoTitle";
import VideoPlayerActionButton from "~/components/VideoPlayerActionButton";

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

// Reactive data
const videoElement = ref(null);
const progressBar = ref(null);
const isPlaying = ref(false);
const currentTime = ref(0);
const duration = ref(0);
const volume = ref(1);
const isMuted = ref(props.muted);
const selectedQuality = ref(props.quality);
const showCenterButton = ref(true);

// Computed properties
const progressPercentage = computed(() => {
  return duration.value ? (currentTime.value / duration.value) * 100 : 0;
});

// Methods
const togglePlay = () => {
  if (videoElement.value) {
    if (isPlaying.value) {
      videoElement.value.pause();
    } else {
      videoElement.value.play();
    }
    isPlaying.value = !isPlaying.value;
    showCenterButton.value = !isPlaying.value;
  }
};

const skipForward = () => {
  if (videoElement.value) {
    videoElement.value.currentTime += 10;
  }
};

const toggleMute = () => {
  if (videoElement.value) {
    videoElement.value.muted = !videoElement.value.muted;
    isMuted.value = videoElement.value.muted;
  }
};

const updateVolume = () => {
  if (videoElement.value) {
    videoElement.value.volume = volume.value;
    isMuted.value = volume.value === 0;
  }
};

const seek = (event) => {
  if (videoElement.value && progressBar.value) {
    const rect = progressBar.value.getBoundingClientRect();
    const percent = (event.clientX - rect.left) / rect.width;
    videoElement.value.currentTime = percent * duration.value;
  }
};

const toggleFullscreen = () => {
  if (videoElement.value) {
    if (document.fullscreenElement) {
      document.exitFullscreen();
    } else {
      videoElement.value.requestFullscreen();
    }
  }
};

const changeQuality = () => {
  // This would typically involve changing video source
  console.log("Quality changed to:", selectedQuality.value);
};

const onLoadedMetadata = () => {
  if (videoElement.value) {
    duration.value = videoElement.value.duration;
  }
};

const onTimeUpdate = () => {
  if (videoElement.value) {
    currentTime.value = videoElement.value.currentTime;
  }
};

const formatTime = (seconds) => {
  const mins = Math.floor(seconds / 60);
  const secs = Math.floor(seconds % 60);
  return `${mins}:${secs.toString().padStart(2, "0")}`;
};

// Keyboard controls
const handleKeydown = (event) => {
  switch (event.code) {
    case "Space":
      event.preventDefault();
      togglePlay();
      break;
    case "ArrowRight":
      event.preventDefault();
      if (videoElement.value) {
        videoElement.value.currentTime += 10;
      }
      break;
    case "ArrowLeft":
      event.preventDefault();
      if (videoElement.value) {
        videoElement.value.currentTime -= 10;
      }
      break;
    case "ArrowUp":
      event.preventDefault();
      volume.value = Math.min(1, volume.value + 0.1);
      updateVolume();
      break;
    case "ArrowDown":
      event.preventDefault();
      volume.value = Math.max(0, volume.value - 0.1);
      updateVolume();
      break;
  }
};

onMounted(() => {
  document.addEventListener("keydown", handleKeydown);
  if (videoElement.value) {
    videoElement.value.volume = volume.value;
    videoElement.value.muted = isMuted.value;
    if (props.autoplay) {
      videoElement.value.play();
      isPlaying.value = true;
      showCenterButton.value = false;
    }
  }
});

onUnmounted(() => {
  document.removeEventListener("keydown", handleKeydown);
});
</script>

<style scoped>
/* Custom slider styles */
.slider::-webkit-slider-thumb {
  appearance: none;
  width: 12px;
  height: 12px;
  border-radius: 50%;
  background: #ef4444;
  cursor: pointer;
}

.slider::-moz-range-thumb {
  width: 12px;
  height: 12px;
  border-radius: 50%;
  background: #ef4444;
  cursor: pointer;
  border: none;
}

/* Hide default video controls */
video::-webkit-media-controls {
  display: none !important;
}

video::-webkit-media-controls-enclosure {
  display: none !important;
}
</style>
