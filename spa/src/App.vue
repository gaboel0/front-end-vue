<template>
  <div id="app">
    <MainPage class="main"/>
  </div>
</template>

<script>
import MainPage from './components/MainPage.vue';

export default {
  name: 'App',
  components: {
    MainPage
  }
}
</script>

<style>

.main {

  max-width: 100%;
}

</style>
