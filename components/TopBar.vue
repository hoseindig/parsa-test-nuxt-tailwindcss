<template>
  <nav class="bg-darkgraybutton text-white px-6 py-4">
    <div class="flex items-center justify-between max-w-7xl mx-auto">
      <!-- Left Side - Navigation Icons -->

      <div class="flex items-center space-x-8">
        <!-- Logo -->
        <div class="flex items-center space-x-2">
          <!-- Shield Logo -->
          <div
            class="w-10 h-10 bg-red-600 rounded-full flex items-center justify-center"
          >
            <svg
              class="w-6 h-6 text-white"
              fill="currentColor"
              viewBox="0 0 20 20"
            >
              <path
                fill-rule="evenodd"
                d="M2.166 4.999A11.954 11.954 0 0010 1.944 11.954 11.954 0 0017.834 5c.11.65.166 1.32.166 2.001 0 5.225-3.34 9.67-8 11.317C5.34 16.67 2 12.225 2 7c0-.682.057-1.35.166-2.001zm11.541 3.708a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z"
                clip-rule="evenodd"
              />
            </svg>
          </div>

          <!-- Brand Text -->
          <div class="text-right">
            <div class="text-red-500 font-bold text-lg leading-tight">
              فیلم<span class="text-white">دانلود</span>
            </div>
            <div class="text-xs text-gray-400 leading-tight">FILM DOWNLOAD</div>
          </div>
        </div>

        <!-- Menu Items -->
        <div class="hidden md:flex items-center space-x-8 text-sm">
          <a href="#" class="hover:text-gray-300 transition-colors"
            >جدید ترین دوبله ها</a
          >
          <a href="#" class="hover:text-gray-300 transition-colors"
            >سریال بازیگران</a
          >
          <a href="#" class="hover:text-gray-300 transition-colors">فیلم</a>
          <a href="#" class="hover:text-gray-300 transition-colors"
            >فیلم بندی ها</a
          >
        </div>
      </div>

      <!-- Right Side - Menu Items and Logo -->
      <div class="flex items-center space-x-6">
        <!-- Notification Bell -->
        <button
          class="p-2 hover:bg-gray-800 rounded-lg transition-colors relative"
        >
          <svg
            class="w-6 h-6"
            fill="none"
            stroke="currentColor"
            viewBox="0 0 24 24"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M15 17h5l-5-5V9.09c0-2.18-1.64-3.96-3.75-4.04C9.26 4.96 8 6.74 8 8.75V12l-5 5h5m5 0v1a3 3 0 11-6 0v-1m6 0H9"
            />
          </svg>
          <!-- Notification Badge -->
          <span
            class="absolute -top-1 -right-1 bg-red-500 text-white text-xs rounded-full w-5 h-5 flex items-center justify-center"
          >
            3
          </span>
        </button>

        <!-- Bookmark Icon -->
        <button class="p-2 hover:bg-gray-800 rounded-lg transition-colors">
          <svg
            class="w-6 h-6"
            fill="none"
            stroke="currentColor"
            viewBox="0 0 24 24"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M5 5a2 2 0 012-2h10a2 2 0 012 2v16l-7-3.5L5 21V5z"
            />
          </svg>
        </button>

        <!-- Search Icon -->
        <button class="p-2 hover:bg-gray-800 rounded-lg transition-colors">
          <svg
            class="w-6 h-6"
            fill="none"
            stroke="currentColor"
            viewBox="0 0 24 24"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"
            />
          </svg>
        </button>

        <!-- User Profile Icon -->
        <button class="p-2 hover:bg-gray-800 rounded-lg transition-colors">
          <svg
            class="w-6 h-6"
            fill="none"
            stroke="currentColor"
            viewBox="0 0 24 24"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z"
            />
          </svg>
        </button>
      </div>
    </div>

    <!-- Mobile Menu Button (visible on smaller screens) -->
    <div class="md:hidden mt-4">
      <button
        class="w-full text-left p-2 hover:bg-gray-800 rounded-lg transition-colors"
      >
        <svg
          class="w-6 h-6"
          fill="none"
          stroke="currentColor"
          viewBox="0 0 24 24"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M4 6h16M4 12h16M4 18h16"
          />
        </svg>
      </button>
    </div>
  </nav>
</template>

<script setup>
// You can add props or reactive data here if needed
</script>

<style scoped>
/* Custom styles for RTL text */
.text-right {
  direction: rtl;
  text-align: right;
}

/* Ensure Persian/Arabic fonts render properly */
* {
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
}
</style>
