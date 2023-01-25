<template>
  <div id="app" class="main-container">
    <div class="main-wrapper">
      <header-bar></header-bar>
      <home-container></home-container>
    </div>
  </div>
</template>

<script>
import HeaderBar from '@/components/HeaderBar.vue';
import HomeContainer from '@/components/Home.vue';

export default {
  name: 'App',
    components: {
      HeaderBar,
      HomeContainer,
  }
}
</script>


<style>
  @import '@/assets/main.css'
</style>