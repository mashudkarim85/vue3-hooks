<script setup>
import Carousel from './components/Carousel.vue'
import PieChart from './components/PieChart.vue'
import { ref } from 'vue'
let currentIndex = ref(0)

function carouselData () {
  currentIndex.value = 0;
}

function pieChartData () {
  currentIndex.value = 1;
}
</script>

<template>
    <div class="flex">
        <button type="button" @click="carouselData"  class="me-3" :class="0==currentIndex ? 'btn btn-primary': ''">Image Carousel</button>
        <button type="button" @click="pieChartData" :class="1==currentIndex ? 'btn btn-primary': ''">Pie Chart</button>
      </div>
    <Carousel v-if="0== currentIndex"/>
    <PieChart  v-if="1== currentIndex"/>
</template>

<style scoped>

</style>
