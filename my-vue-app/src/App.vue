<script setup>
// setup 生命周期等同于beforecreate+created+data函数,不涉及dom渲染
import * as echarts from "echarts";
import Testoption from "./Testoption";
import { onBeforeMount, onBeforeUnmount, onMounted } from "vue";

let resize = (chart) => {
  chart.resize();

}
let chart_instance;
const init_charts = async () => {

  // try {
  //   let data = await fetch("../public/grades.json");
  //   let map_data = await data.json();
  //   console.log("data"+map_data);
  // } catch (e) {
  //   console.log("错误！",e);
  // }

  
  const ele = document.querySelector('#map-chart');







  // 初始化
  chart_instance = echarts.init(ele);
  chart_instance.setOption(Testoption);

  // 预先绑定参数
  resize = resize.bind('asThis', chart_instance);
  window.addEventListener("resize", resize);

}
onBeforeUnmount(() => {
  window.removeEventListener('resize', resize);
})
onMounted(init_charts);
</script>

<template>
  <div id="map-chart"></div>
</template>

<style scoped>
html,
body,
#app {
  width: 100vw;
  height: 100vh;
}

#map-chart {
  width: 100%;
  height: 600px;
}
</style>
