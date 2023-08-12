<template>
  <div class="justify-center mt-5">
    <h3>Vue Pie Chart Example</h3>
    <GChart
      type="PieChart"
      :options="options"
      :data="data"
    />    
  </div>
</template>
 
<script setup>
import { onMounted, onBeforeUnmount } from "vue";
import { GChart } from "vue-google-charts";

const data = [
  ['Daily Routine', 'Hours per Day'],
  ['Work',     14],
  ['Eat',      1],
  ['Reading',  2]
  
];

const options = {
  width: 1000,
  height: 600
};

onMounted(() => {
  console.log('Pie chart onMounted hooks call')
  data.push(['Exercise', 2], ['Sleep',    5])
})

onBeforeUnmount(() => {
  console.log('Pie chart onBeforeUnmount hooks call')
  data.splice(4, 2);
});

</script>