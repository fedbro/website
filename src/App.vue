<template>
  <div id="app">
    <Navbar />
    <main class="main">
      <div  class="home__bg">
        <router-view />
      </div>
    </main>
  </div>
</template>

<script>
import Navbar from "./components/Navbar";
export default {
  
  components: {
    Navbar,
  },
  
};
</script>

<style>
  @import './assets/scss/styles.css';
</style>

