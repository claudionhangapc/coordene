<template>
  <div id="app">
    <BestTransport/>
    <MainSection/>
  </div>
</template>

<script>
import BestTransport from './components/BestTransport.vue'
import MainSection from './components/MainSection.vue'
export default {
  name: 'App',
  components: {
    BestTransport,
    MainSection
  }
}
</script>

<style>
</style>
