<template>
  <section id="home" class="flex items-center justify-center min-h-screen bg-white">
    <div class="container mx-auto px-6 flex flex-col md:flex-row items-center justify-between">
      <!-- Left Column - Text Content -->
      <div class="md:w-1/2 mb-10 md:mb-0 space-y-4">
        <h1 class="text-4xl md:text-5xl font-light text-gray-900">John <span class="font-medium">Doe</span></h1>
        <p class="text-xl text-gray-600 border-l-4 border-blue-500 pl-4 py-1">Web Developer</p>
        <p class="text-gray-700 max-w-md leading-relaxed">Crafting digital experiences with clean code and thoughtful design. Currently focused on modern web technologies and user-centric solutions.</p>
        <button class="mt-6 px-6 py-2 bg-transparent border border-gray-800 text-gray-800 hover:bg-gray-800 hover:text-white transition-colors duration-300">View My Work</button>
      </div>

      <!-- Right Column - Profile Image -->
      <div class="md:w-1/2 flex justify-center">
        <div class="relative w-64 h-64 md:w-80 md:h-80 overflow-hidden rounded-lg">
          <img src="https://images.unsplash.com/photo-1507003211169-0a1dd7228f2d?ixlib=rb-1.2.1&auto=format&fit=crop&w=634&q=80" alt="John Doe" class="w-full h-full object-cover grayscale hover:grayscale-0 transition-all duration-500" />
          <div class="absolute inset-0 border-2 border-gray-200 rounded-lg m-2 pointer-events-none"></div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
// Component logic can be added here if needed
</script>

<style scoped>
/* Custom transitions */
.transition-colors {
  transition: background-color 0.3s ease, color 0.3s ease;
}
</style>
