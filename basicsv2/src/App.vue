<template>
  <div id="app">
    <div class="logo-container">
      <img alt="Vue logo" src="./assets/logo.png">
      <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    </div>
    <BasicsComponent />
  </div>
</template>

<script>
import BasicsComponent from './components/BasicsComponent.vue';
// import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    // HelloWorld,
    BasicsComponent
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  color: #2c3e50;
  margin-top: 60px;
}
.logo-container {
  text-align: center;
}
</style>
