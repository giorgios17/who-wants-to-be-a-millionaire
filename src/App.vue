<template>
  <div id="app">
    <ContainerApp />
  </div>
</template>

<script>
import ContainerApp from "./components/ContainerApp.vue";

export default {
  name: "App",
  components: {
    ContainerApp,
  },
};
</script>

<style lang="scss">
@import "../src/assets/style/reset.scss";
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: white;
}
</style>
