<script>
import HomeView from './views/HomeView.vue';
import CustomHeader from './components/CustomHeader.vue'

export default {
  components: {
    HomeView,
    CustomHeader,
  }
} 
</script>

<template>
  <main>
    <custom-header />
    <router-view class="app"></router-view>
  </main>
</template>

<style>
</style>