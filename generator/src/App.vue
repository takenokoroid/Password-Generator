<template>
  <div class="container">
    <GeneratorHome />
  </div>
</template>

<script>
import GeneratorHome from "./components/GeneratorHome.vue";

export default {
  name: "App",
  components: {
    GeneratorHome,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  padding-top: 60px;
  background-color: #15202b;
  height: 100vh;
}
</style>
