<template>
  <nav class="text-white py-3 px-6">
    <div class="mx-auto">
      <button
        @click="goBack"
        class="flex items-center space-x-2 space-x-reverse text-white hover:text-gray-300 transition-colors group"
      >
        <!-- Back Arrow Icon -->
        <span class="text-sm font-medium">{{ backText }}</span>

        <!-- Back Text -->
        <svg
          class="w-5 h-5 transform group-hover:translate-x-1 transition-transform duration-200"
          fill="none"
          stroke="currentColor"
          viewBox="0 0 24 24"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M15 19l-7-7 7-7"
          />
        </svg>
      </button>
    </div>
  </nav>
</template>

<script setup>
import { defineEmits, defineProps } from "vue";

// Props
const props = defineProps({
  backText: {
    type: String,
    default: "بازگشت",
  },
  // Optional: custom route to go back to
  backRoute: {
    type: String,
    default: null,
  },
});

// Emits
const emit = defineEmits(["back"]);

// Methods
const goBack = () => {
  if (props.backRoute) {
    // If custom route is provided, navigate to it
    // You can use Vue Router here
    // router.push(props.backRoute)
    emit("back", props.backRoute);
  } else {
    // Default browser back behavior
    window.history.back();
    emit("back");
  }
};
</script>

<style scoped>
/* Ensure proper RTL support */
* {
  direction: rtl;
  font-family: "Segoe UI", "Iranian Sans", "B Yekan", Tahoma, Arial, sans-serif;
}

/* Custom spacing for RTL */
.space-x-reverse > :not([hidden]) ~ :not([hidden]) {
  --tw-space-x-reverse: 1;
  margin-right: calc(0.5rem * var(--tw-space-x-reverse));
  margin-left: calc(0.5rem * calc(1 - var(--tw-space-x-reverse)));
}
</style>
