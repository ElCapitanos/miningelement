<template>
  <div class="range">
    <range-color-part
      v-for="(color, index) in colors"
      :key="index"
      :color="color"
      :data="data"
      :title="title"
      class="range__color-part"
    />
  </div>
</template>
<script>
import RangeColorPart from "./RangeColorPart.vue";
export default {
  name: "RangePartComponenth",
  data() {
    return {
      colors: ["#45E596", "#FFC44C", "#FF4C4C"],
    };
  },
  components: { RangeColorPart },
  props: ["data", "title"],
  methods: {
  },
};
</script>
<style lang="scss" scoped>
.range {
  display: flex;
  flex-direction: row;
  justify-content: flex-start;
  width: 100%;
  height: 6px;
  background-color: #ccc;
  margin: auto 0;
}
.range:hover .range__color-part:not(:hover) {
  opacity: 0.08;
  transition: 0.4s linear;
}
@media screen and (max-width: 600px) {
  .range {
    width: 70%;
  }
}
</style>
