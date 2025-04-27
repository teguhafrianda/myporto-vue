<template>
  <section id="projects" class="relative min-h-screen bg-gray-50 overflow-hidden">
    <!-- Animated background elements -->
    <div class="absolute inset-0 overflow-hidden">
      <div class="absolute top-0 left-0 w-64 h-64 bg-green-100 rounded-full mix-blend-multiply filter blur-3xl opacity-70 animate-blob"></div>
      <div class="absolute top-0 right-0 w-64 h-64 bg-yellow-100 rounded-full mix-blend-multiply filter blur-3xl opacity-70 animate-blob animation-delay-2000"></div>
      <div class="absolute bottom-0 right-0 w-64 h-64 bg-red-100 rounded-full mix-blend-multiply filter blur-3xl opacity-70 animate-blob animation-delay-4000"></div>
    </div>

    <div class="container mx-auto px-6 py-24 relative z-10">
      <!-- Section title with scroll animation -->
      <h2 class="text-4xl md:text-5xl font-bold text-gray-800 mb-16 text-center" v-animate-on-scroll="{ animation: 'fadeInUp', duration: 800 }">Projects</h2>

      <!-- Project list container -->
      <div class="relative">
        <!-- Vertical line -->
        <div class="absolute left-1/2 w-1 h-full bg-gray-300 transform -translate-x-1/2"></div>

        <!-- Project items -->
        <div
          v-for="(project, index) in projectItems"
          :key="index"
          class="mb-16"
          v-animate-on-scroll="{
            animation: index % 2 === 0 ? 'fadeInLeft' : 'fadeInRight',
            duration: 800,
            delay: index * 100,
          }"
        >
          <div class="flex flex-col md:flex-row items-center" :class="{ 'md:flex-row-reverse': index % 2 !== 0 }">
            <!-- Project title -->
            <div class="w-full md:w-1/2 px-6 py-4 text-center md:text-left" :class="{ 'md:text-right': index % 2 === 0 }">
              <p class="text-lg font-semibold text-blue-600">{{ project.name }}</p>
            </div>

            <!-- Project details -->
            <div class="w-full md:w-1/2 px-6 py-4">
              <div class="bg-white p-6 rounded-xl shadow-lg hover:shadow-xl transition-shadow duration-300">
                <h3 class="text-xl font-bold text-gray-800 mb-2">{{ project.title }}</h3>
                <p class="text-gray-600">{{ project.description }}</p>
                <div v-if="project.technologies" class="mt-3 flex flex-wrap gap-2">
                  <span v-for="(tech, techIndex) in project.technologies" :key="techIndex" class="px-3 py-1 bg-gray-100 text-gray-700 rounded-full text-sm">
                    {{ tech }}
                  </span>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted } from "vue";

// Project items for the projects section
const projectItems = ref([
  {
    name: "Aplikasi Kasir",
    title: "Fullstack Laravel POS System",
    description: "Aplikasi kasir berbasis web dengan fitur manajemen produk, transaksi, laporan penjualan, dan multi-user roles. Dibangun menggunakan Laravel dan Vue.js.",
    technologies: ["Laravel", "Vue 3", "MySQL", "REST API"],
  },
  {
    name: "NLC Application",
    title: "Event Management Platform with DDD",
    description: "Platform registrasi dan manajemen kompetisi untuk National Level Competition menggunakan Laravel dengan pendekatan Domain-Driven Design (DDD).",
    technologies: ["Laravel", "DDD", "PostgreSQL", "Clean Architecture"],
  },
]);

// Scroll animation directive
const vAnimateOnScroll = {
  mounted(el, binding) {
    const options = {
      threshold: 0.1,
      rootMargin: "0px",
    };

    const observer = new IntersectionObserver((entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          el.style.opacity = 0;
          el.style.animation = `${binding.value.animation} ${binding.value.duration}ms forwards ${binding.value.delay || 0}ms`;
          observer.unobserve(el);
        }
      });
    }, options);

    observer.observe(el);
  },
};

onMounted(() => {
  // Register the scroll animation directive globally
  app.directive("animate-on-scroll", vAnimateOnScroll);
});
</script>

<style>
/* Animation Styles */
@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes fadeInLeft {
  from {
    opacity: 0;
    transform: translateX(-50px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

@keyframes fadeInRight {
  from {
    opacity: 0;
    transform: translateX(50px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

@keyframes blob {
  0% {
    transform: translate(0px, 0px) scale(1);
  }
  33% {
    transform: translate(30px, -50px) scale(1.1);
  }
  66% {
    transform: translate(-20px, 20px) scale(0.9);
  }
  100% {
    transform: translate(0px, 0px) scale(1);
  }
}

.animate-blob {
  animation: blob 7s infinite;
}

.animation-delay-2000 {
  animation-delay: 2s;
}

.animation-delay-4000 {
  animation-delay: 4s;
}

[v-animate-on-scroll] {
  opacity: 0;
}
</style>
