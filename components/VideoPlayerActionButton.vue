<template>
  <nav class="text-white py-4 px-6">
    <div class="max-w-7xl mx-auto">
      <div class="flex items-center justify-between">
        <!-- Left Side - Logo/Brand Text -->
        <div class="flex items-center space-x-4 space-x-reverse">
          <!-- Samsung TV Link - Active/Highlighted -->
          <a
            href="#"
            class="h-12 flex items-center bg-red-600 hover:bg-red-700 px-4 rounded-md text-white font-medium text-sm transition-colors"
          >
            پلیر تلویزیون های سامسونگ
          </a>

          <!-- Other Navigation Links -->
          <a
            href="#"
            class="h-12 flex items-center text-gray-300 hover:text-white px-4 text-sm transition-colors"
          >
            پلیر تلویزیون های قدیمی
          </a>

          <a
            href="#"
            class="h-12 flex items-center text-gray-300 hover:text-white px-4 text-sm transition-colors"
          >
            پلیر تلویزیون های قدیمی
          </a>
        </div>

        <!-- Right Side - Navigation Links -->
        <div class="hidden md:block text-gray-300 text-sm">
          حین تماشا با مشکلی رو به رو شدید؟
        </div>
        <!-- Center - Question Text -->

        <div class="text-white font-medium">اعلام مشکل</div>
      </div>

      <!-- Mobile Menu (visible on smaller screens) -->
      <div class="md:hidden mt-4 space-y-2">
        <!-- Question text for mobile -->
        <div class="text-gray-300 text-sm text-center mb-4">
          حین تماشا با مشکلی رو به رو شدید؟
        </div>

        <!-- Mobile navigation links -->
        <div class="flex flex-col space-y-2">
          <a
            href="#"
            class="bg-red-600 hover:bg-red-700 px-4 py-2 rounded-md text-white font-medium text-sm text-center transition-colors"
          >
            پلیر تلویزیون های سامسونگ
          </a>

          <a
            href="#"
            class="text-gray-300 hover:text-white px-4 py-2 text-sm text-center transition-colors"
          >
            پلیر تلویزیون های قدیمی
          </a>

          <a
            href="#"
            class="text-gray-300 hover:text-white px-4 py-2 text-sm text-center transition-colors"
          >
            پلیر تلویزیون های قدیمی
          </a>
        </div>
      </div>
    </div>
  </nav>
</template>

<script setup>
import { ref } from "vue";

// Optional: Add reactive data for active link
const activeLink = ref("samsung");

// Optional: Add props for customization
const props = defineProps({
  brandText: {
    type: String,
    default: "اعلام مشکل",
  },
  questionText: {
    type: String,
    default: "چین تماشا با مشکلی رو به رو شدید؟",
  },
  links: {
    type: Array,
    default: () => [
      { id: "samsung", text: "پلیر تلویزیون های سامسونگ", active: true },
      { id: "old1", text: "پلیر تلویزیون های قدیمی", active: false },
      { id: "old2", text: "پلیر تلویزیون های قدیمی", active: false },
    ],
  },
});

// Optional: Add method to handle link clicks
const handleLinkClick = (linkId) => {
  activeLink.value = linkId;
  // Emit event or handle navigation
};
</script>

<style scoped>
/* Ensure proper RTL support and Persian font rendering */
* {
  direction: rtl;
  font-family: "Segoe UI", "Iranian Sans", "B Yekan", Tahoma, Arial, sans-serif;
}

/* Custom spacing for RTL */
.space-x-reverse > :not([hidden]) ~ :not([hidden]) {
  --tw-space-x-reverse: 1;
  margin-right: calc(1rem * var(--tw-space-x-reverse));
  margin-left: calc(1rem * calc(1 - var(--tw-space-x-reverse)));
}
</style>
