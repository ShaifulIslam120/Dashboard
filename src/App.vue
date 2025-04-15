<template>
  <v-app>
    <NavBar />
    <v-main class="bg-gray-50">
      <div class="w-full px-4 md:w-11/12 mx-auto">
        <Overview />
        <Movies></Movies>
        <TrendingMovies></TrendingMovies>
      </div>
    </v-main>
    <Footer />
  </v-app>
</template>

<script setup>
import Movies from './components/Movies.vue';
import NavBar from './components/NavBar.vue'
import Overview from './components/Overview.vue';
import TrendingMovies from './components/TrendingMovies.vue';
import Footer from './components/Footer.vue';
</script>