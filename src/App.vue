<template>
  <div class="app-container">
    <NavBar />
    <Home />
    <FooterSection />
  </div>
</template>

<script>
import NavBar from './components/NavBar.vue'
import Home from './views/Home.vue'
import FooterSection from './components/FooterSection.vue'

export default {
  name: 'App',
  components: {
    NavBar,
    Home,
    FooterSection
  }
}
</script>

<style>
.app-container {
  position: relative;
  min-height: 100vh;
  overflow: hidden;
}
</style>