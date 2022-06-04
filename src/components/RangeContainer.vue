<template>
  <article class="container">
    <range-component />
  </article>
</template>
<script>
import RangeComponent from "./RangeComponent.vue";
export default {
  name: "RangeContainer",
  components: {
    RangeComponent,
  },
};
</script>
<style lang="scss" scoped>
.container {
  display: flex;
  width: 98%;
  margin: 10px auto;
  background-color: #fff;
  border: 1px solid transparent;
  border-radius: 4px;
  box-sizing: border-box;
  flex-direction: row;
  flex-wrap: wrap;
  padding: 0 8px;
  justify-content: space-around;
}
</style>
