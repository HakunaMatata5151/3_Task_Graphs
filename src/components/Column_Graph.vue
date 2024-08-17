<script setup>

import { ref, onMounted } from 'vue'
import {
  Chart as ChartJS, Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale
} from 'chart.js'
import { Bar } from 'vue-chartjs'
import * as chartConfig from '@/lib/columnChartConfig'

ChartJS.register(Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale)

const options = chartConfig.options
const data = ref({
  datasets: []
})

const emit = defineEmits(["done"]);

onMounted(() => {
  data.value = chartConfig.randomData()
  emit('done')
})


</script>

<template>
  <div>
    <Bar :data="data" :options="options" />
  </div>
</template>

<style scoped></style>
