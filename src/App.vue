<template>
  <div id="app">
    <MainBlock />
  </div>
</template>

<script>
import MainBlock from "./components/MainBlock.vue";

export default {
  name: "app",
  components: {
    MainBlock
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
