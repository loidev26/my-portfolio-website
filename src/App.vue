<script setup>
  import Navbar from './components/Navbar.vue'
  import Landing from './components/Landing.vue'
  import Education from './components/Education.vue'
  import Projects from './components/Projects.vue'
  import Tools from './components/Tools.vue'
  import Contact from './components/Contact.vue'
  import Footer from './components/Footer.vue'
  import { ref, onMounted, onUnmounted } from 'vue';

  const showButton = ref(false);

  // Show button when scrolling down
  function scrollFunction() {
      showButton.value = window.scrollY > 20;
  }

  // Scroll back to the top
  function topFunction() {
      window.scrollTo({
          top: 0,
          behavior: 'smooth'
      });
  }

  // Add scroll listener when component loads
  onMounted(() => {
      window.addEventListener('scroll', scrollFunction);
  });

  // Remove listener when component is destroyed
  onMounted(() => {
      window.addEventListener('scroll', scrollFunction);
      scrollFunction(); // Check the current scroll position immediately
  });
</script>

<template>
  <Navbar />
  <Landing />
  <Education />
  <Projects />
  <Tools />
  <Contact />
  <Footer />
  <!-- Scroll To Top Button -->
  <button
      v-show="showButton"
      @click="topFunction"
      id="myBtn"
      title="Go to top"
  >
      Top
  </button>
</template>