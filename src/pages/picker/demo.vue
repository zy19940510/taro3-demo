<template>
  <div class="demo">
    <h2>多列样式</h2>
    <nut-picker mode="multiSelector" :list-data="listData2" @confirm="confirm2">
      <nut-cell title="请选择时间" :desc="desc2"></nut-cell>
    </nut-picker>
  </div>
</template>
<script lang="ts">
import { ref } from "vue";
import { createComponent } from "../utils/create";
import Picker from "./index.taro.vue";
import Cell from "./../cell/index.taro.vue";
const { createDemo } = createComponent("picker");
export default createDemo({
  components: {
    "nut-picker": Picker,
    "nut-cell": Cell,
  },
  props: {},
  setup() {
    const listData2 = ref([
      {
        values: ["周一", "周二", "周三", "周四", "周五"],
        defaultIndex: 2,
      },
      {
        values: ["上午", "下午", "晚上"],
        defaultIndex: 1,
      },
    ]);

    const desc2 = ref(
      `${listData2.value[0].values[listData2.value[0].defaultIndex]} ${
        listData2.value[1].values[listData2.value[1].defaultIndex]
      }`
    );

    const confirm2 = (value, res: any) => {
      desc2.value = res.join(" ");
      listData2.value.forEach((item, idx) => {
        item.defaultIndex = value[idx];
      });
    };

    return {
      listData2,
      desc2,
      confirm2,
    };
  },
});
</script>
