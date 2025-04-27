<script setup>
import Navbar from "./components/Navbar.vue";
import Home from "./components/Home.vue";
import About from "./components/About.vue";
import Projects from "./components/Projects.vue";
</script>

<template>
  <div>
    <!-- Navbar untuk navigasi -->
    <Navbar />

    <!-- Konten utama -->
    <section id="home">
      <Home />
    </section>

    <section id="about">
      <About />
    </section>

    <section id="projects">
      <Projects />
    </section>
  </div>
</template>

<style scoped>
/* Gaya khusus jika diperlukan */
</style>
