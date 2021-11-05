<template>
  <div class="charts">
    <div ref="echartRef" :style="{ height: height, width: width }"></div>
  </div>
</template>

<script setup lang="ts">
import { defineProps, withDefaults, watch, defineExpose } from "vue";
import useEcharts from "../hooks/use-echarts";
import { EChartsOption } from "echarts";

// 定義props
const props = withDefaults(
  defineProps<{
    options: EChartsOption;
    width?: string;
    height?: string;
  }>(),
  {
    width: "100%",
    height: "360px",
  }
);

const { echartRef, setOptions, updateSize } = useEcharts(props.options);

const sss: EChartsOption = {
  tooltip: {
    trigger: "item",
  },
  legend: {
    orient: "horizontal",
    left: "left",
  },
  series: [
    {
      name: "商品數量",
      type: "pie",
      radius: "50%",
      // data: props.pieData,
      emphasis: {
        itemStyle: {
          shadowBlur: 10,
          shadowOffsetX: 0,
          shadowColor: "rgba(0, 0, 0, 0.5)",
        },
      },
    },
  ],
};

watch(
  () => props.options,
  () => {
    setOptions(props.options);
  }
);

defineExpose({
  updateSize,
});
</script>

<style scoped></style>
