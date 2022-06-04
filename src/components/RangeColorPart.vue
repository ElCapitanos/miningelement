<template>
  <div
    ref="currentRange"
    class="color-part"
    :style="inputStyle"
    @mouseenter="partToggleHover"
    @mouseleave="partToggleHover"
  >
    <span v-if="hoverFlag" class="color-part__legend color-part__legend_up">{{
      width
    }}</span>
    <span v-if="hoverFlag" class="color-part__legend color-part__legend_down"
      >{{ currentVal }} из {{ data.length }}</span
    >
  </div>
</template>
<script>
export default {
  name: "RangeColorPart",
  data() {
    return {
      width: null,
      hoverFlag: false,
      currentVal: null,
    };
  },
  props: ["color", "data", "title"],
  components: {},
  computed: {
    inputStyle() {
      return { "--color": this.color, "--width": this.width };
    },
  },

  methods: {
    partToggleHover() {
      this.hoverFlag = !this.hoverFlag;
    },
    rangePartsWidth(arr, minVal, MaxVal) {
      let newArr = arr.filter((item) => item > minVal && item < MaxVal);
      this.currentVal = newArr.length;
      return Math.round((newArr.length / arr.length) * 100);
    },
    switcCaseColor(
      color,
      greenMin,
      greenMax,
      yellowMin,
      yellowMax,
      redMin,
      redMax
    ) {
      switch (color) {
        case "#45E596":
          this.width =
            this.rangePartsWidth(this.data, greenMin, greenMax) + "%";
          break;
        case "#FFC44C":
          this.width =
            this.rangePartsWidth(this.data, yellowMin, yellowMax) + "%";
          break;
        case "#FF4C4C":
          this.width = this.rangePartsWidth(this.data, redMin, redMax) + "%";
          break;
      }
    },
    getCurrentWidth(color) {
      if (this.title != "quantity") {
        this.switcCaseColor(color, 0, 500, 501, 1000, 1001, 100000);
      } else {
        this.switcCaseColor(color, 0, 2, 1, 3, 2, 10000);
      }
    },
  },
  mounted() {
    this.getCurrentWidth(this.color);
  },
  updated() {
    this.getCurrentWidth(this.color);
  },
};
</script>
<style lang="scss" scoped>
.color-part {
  position: relative;
  height: 100%;
  display: flex;
  min-width: 8px;
  background-color: var(--color);
  width: var(--width);
  cursor: pointer;
}
.color-part__legend {
  position: absolute;
  width: fit-content;
  padding: 0 6px;
  left: 50%;
  transform: translateX(-50%);
  font-size: 8px;
  display: flex;
}
.color-part__legend_up {
  top: -12px;
}
.color-part__legend_down {
  bottom: -12px;
}
</style>
