<template>
  <article class="app">
    <range-container />
  </article>
</template>

<script>
import RangeContainer from "./components/RangeContainer.vue";
export default {
  name: "App",
  components: {
    RangeContainer,
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.app {
  width: 100%;
  height: 100%;
  position: fixed;
  top: 0;
  left: 0;
  background-color: #ccc;
}
</style>
