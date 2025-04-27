<template>
  <div class="fixed z-40 bg-gray-700 h-14 w-[50vw] flex justify-between items-center p-4 top-0 left-1/2 transform -translate-x-1/2 rounded-b-3xl">
    <ul class="flex justify-evenly items-center w-full text-gray-50">
      <li v-for="(item, index) in navItems" :key="index">
        <a :href="item.path" class="p-2 rounded-full hover:bg-gray-600 transition-colors duration-200 flex items-center justify-center" :class="{ 'bg-gray-600': activeSection === item.path }" @click.prevent="scrollToSection(item.path)">
          <FontAwesomeIcon :icon="item.icon" class="text-xl" />
          <span class="sr-only">{{ item.name }}</span>
        </a>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
import { faHome, faUser, faFolderOpen, faEnvelope } from "@fortawesome/free-solid-svg-icons";

const activeSection = ref("#home");

const navItems = [
  { name: "Home", path: "#Home", icon: faHome },
  { name: "About", path: "About", icon: faUser },
  { name: "Projects", path: "#projects", icon: faFolderOpen },
  { name: "Contact", path: "#contact", icon: faEnvelope },
];

const scrollToSection = (sectionId) => {
  const section = document.querySelector(sectionId);
  if (section) {
    section.scrollIntoView({ behavior: "smooth" });
    activeSection.value = sectionId;
  }
};

// Update active section on scroll
onMounted(() => {
  window.addEventListener("scroll", () => {
    navItems.forEach((item) => {
      const section = document.querySelector(item.path);
      if (section) {
        const rect = section.getBoundingClientRect();
        if (rect.top <= 100 && rect.bottom >= 100) {
          activeSection.value = item.path;
        }
      }
    });
  });
});
</script>

<style scoped>
/* Smooth transition for active state */
a {
  transition: background-color 0.3s ease;
}

/* Accessibility focus styles */
a:focus {
  outline: none;
  box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.5);
}
</style>
