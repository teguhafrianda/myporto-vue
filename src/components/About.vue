<template>
  <section id="about" class="relative min-h-screen bg-white px-6 md:px-32 overflow-hidden">
    <!-- Animated background elements -->
    <div class="absolute inset-0 overflow-hidden z-0">
      <div class="absolute top-0 left-0 w-64 h-64 bg-blue-50 rounded-full mix-blend-multiply filter blur-3xl opacity-50 animate-blob"></div>
      <div class="absolute bottom-0 right-0 w-64 h-64 bg-purple-50 rounded-full mix-blend-multiply filter blur-3xl opacity-50 animate-blob animation-delay-2000"></div>
    </div>

    <div class="relative z-10 flex flex-col items-center justify-center min-h-screen py-20">
      <!-- Title with animation -->
      <div class="w-full mb-16" v-animate-on-scroll="{ animation: 'fadeInUp', duration: 800 }">
        <div class="flex flex-col items-start">
          <div class="w-32 h-1.5 bg-blue-500 rounded-full mb-4"></div>
          <h1 class="text-4xl md:text-5xl font-bold text-gray-900">Who <span class="text-blue-500">Am I?</span></h1>
        </div>
      </div>

      <!-- Content with staggered animations -->
      <div class="w-full grid grid-cols-1 lg:grid-cols-2 gap-12 items-center">
        <!-- Images with parallax effect -->
        <div class="relative h-[400px] md:h-[500px]" v-animate-on-scroll="{ animation: 'fadeInLeft', duration: 800 }">
          <div class="absolute inset-0 flex items-center justify-center">
            <div class="relative w-3/4 h-3/4">
              <!-- Main image -->
              <img
                src="https://images.unsplash.com/photo-1507003211169-0a1dd7228f2d?ixlib=rb-1.2.1&auto=format&fit=crop&w=634&q=80"
                alt="Profile"
                class="absolute inset-0 w-full h-full object-cover rounded-2xl shadow-xl border-4 border-white transform hover:scale-105 transition-all duration-500 grayscale hover:grayscale-0"
                data-parallax
                data-speed="0.1"
              />

              <!-- Decorative elements -->
              <div class="absolute -bottom-6 -right-6 w-32 h-32 bg-blue-500 rounded-2xl -z-10"></div>
              <div class="absolute -top-6 -left-6 w-24 h-24 bg-purple-500 rounded-xl -z-10"></div>
            </div>
          </div>
        </div>

        <!-- Biodata with typewriter effect -->
        <div class="space-y-6" v-animate-on-scroll="{ animation: 'fadeInRight', duration: 800, delay: 200 }">
          <h2 class="text-3xl md:text-4xl font-bold text-gray-900"><span class="text-blue-500">Alvalen</span> Shafelbilyunazra</h2>

          <div class="space-y-4 text-gray-700 text-lg leading-relaxed">
            <p>
              <span class="typewriter" data-text="Hi! I'm Alvalen Shafelbilyunazra"></span>, a passionate <span class="font-semibold text-blue-600">Physics Graduate</span> and
              <span class="font-semibold text-purple-600">Web Developer Enthusiast</span> from Padang, Indonesia.
            </p>

            <p>Currently pursuing my Master's degree at <span class="font-semibold">Universitas Negeri Malang</span>, with a focus on <span class="highlight">technology</span> and <span class="highlight">innovation</span>.</p>

            <p>
              My expertise spans <span class="font-semibold text-blue-600">Laravel development</span>, <span class="font-semibold text-purple-600">industrial tech</span>, and exploring the beauty of
              <span class="font-semibold">software engineering</span>.
            </p>

            <p class="text-gray-900 font-medium">I believe in continuous learning to thrive in our fast-evolving digital world.</p>
          </div>

          <!-- Skills tags -->
          <div class="flex flex-wrap gap-3 pt-4">
            <span
              v-for="(skill, index) in skills"
              :key="index"
              class="px-4 py-2 bg-white border border-gray-200 rounded-full text-sm font-medium shadow-sm hover:shadow-md transition-all duration-300 hover:-translate-y-1"
              v-animate-on-scroll="{ animation: 'fadeInUp', duration: 500, delay: 300 + index * 100 }"
            >
              {{ skill }}
            </span>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { onMounted } from "vue";

const skills = ["Laravel", "Vue.js", "Tailwind CSS", "Physics", "Research", "Industrial Tech", "Software Engineering", "Innovation"];

// Scroll animation directive
const vAnimateOnScroll = {
  mounted(el, binding) {
    const observer = new IntersectionObserver(
      (entries) => {
        entries.forEach((entry) => {
          if (entry.isIntersecting) {
            el.style.animation = `${binding.value.animation} ${binding.value.duration}ms forwards ${binding.value.delay || 0}ms`;
            observer.unobserve(el);
          }
        });
      },
      { threshold: 0.1 }
    );

    observer.observe(el);
  },
};

// Parallax effect
onMounted(() => {
  const parallaxElements = document.querySelectorAll("[data-parallax]");

  const handleScroll = () => {
    parallaxElements.forEach((element) => {
      const speed = parseFloat(element.dataset.speed);
      const yPos = -window.scrollY * speed;
      element.style.transform = `translateY(${yPos}px)`;
    });
  };

  window.addEventListener("scroll", handleScroll);

  // Typewriter effect
  const typewriterElements = document.querySelectorAll(".typewriter");
  typewriterElements.forEach((el) => {
    const text = el.dataset.text;
    let i = 0;
    const typing = setInterval(() => {
      if (i < text.length) {
        el.innerHTML += text.charAt(i);
        i++;
      } else {
        clearInterval(typing);
      }
    }, 50);
  });
});
</script>

<style scoped>
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
    transform: translate(0, 0) scale(1);
  }
  33% {
    transform: translate(30px, -30px) scale(1.1);
  }
  66% {
    transform: translate(-20px, 20px) scale(0.9);
  }
  100% {
    transform: translate(0, 0) scale(1);
  }
}

.animate-blob {
  animation: blob 8s infinite ease-in-out;
}

.animation-delay-2000 {
  animation-delay: 2s;
}

[v-animate-on-scroll] {
  opacity: 0;
}

.highlight {
  background: linear-gradient(120deg, #a0c4ff 0%, #bdb2ff 100%);
  background-repeat: no-repeat;
  background-size: 100% 40%;
  background-position: 0 90%;
}

.typewriter {
  display: inline-block;
  overflow: hidden;
  border-right: 2px solid #3b82f6;
  white-space: nowrap;
  animation: blink-caret 0.75s step-end infinite;
}

@keyframes blink-caret {
  from,
  to {
    border-color: transparent;
  }
  50% {
    border-color: #3b82f6;
  }
}
</style>
