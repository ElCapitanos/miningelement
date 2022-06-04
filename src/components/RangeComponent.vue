<template>
  <div class="item" v-for="(item, key) in dataArr" :key="key">
    <span class="item__title">{{ firstLetter(key) }}</span>
    <range-part-component v-if="loadFlag" :data="item" :title="key" class="item__part"/>
    <pulse-loader class="item__loader" v-else :color="loaderColor" :size="size"></pulse-loader>
  </div>
</template>
<script>
import { currentUrl } from "../data";
import RangePartComponent from "./RangePartComponent.vue";
import PulseLoader from 'vue-spinner/src/PulseLoader.vue'
export default {
  components: {
    RangePartComponent,
    PulseLoader,
  },
  name: "RangeComponent",
  data() {
    return {
      loaderColor: '#ccc',
      loadFlag: false,
      dataArr: {
        price: [],
        discountedPrice: [],
        quantity: [],
        total: [],
      },
      currentUrl,
    };
  },
  computed: {},
  methods: {
    firstLetter(str) {
      if (!str) return str;
      return str[0].toUpperCase() + str.slice(1);
    },
    getDataArr(newArr, arr) {
      for (let key in newArr) {
        this.getAllParamsValue(newArr, key, arr);
      }
    },
    getAllParamsValue(newArr, key, arr) {
      for (let i = 0; i < arr.length; i++) {
        for (let j = 0; j < arr[i].products.length; j++) {
          newArr[key].push(+arr[i].products[j][key]);
        }
      }
    },
    getData(url) {
      fetch(url)
        .then((res) => res.json())
        .then((data) => {
          this.loadFlag = true
          this.getDataArr(this.dataArr, data.carts); // не совсем универсальная ф-ция, т.к. data.carts, а не data
        });
    },
  },
  mounted() {
    this.getData(currentUrl);
  },
};
</script>
<style lang="scss" scoped>
.item {
  width: 48%;
  height: 66px;
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  padding: 0 4px;
  min-width: 300px;
  margin: 5px auto;
  justify-content: space-between;
}
.item__title {
  width: 20%;
  display: flex;
  font-size: 12px;
  font-weight: 400;
  margin: auto 6px auto 0;
}
.item__loader {
  display: flex;
  margin: auto;
}
@media screen and (max-width: 740px) {
  .item {
    width: 98%;
    min-width: 300px;
  }
  .item__title {
    width: 15%;
  }
}
</style>
