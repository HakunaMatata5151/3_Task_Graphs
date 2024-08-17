<script setup>
import { onMounted } from 'vue';
import {
    Chart as ChartJS,
    CategoryScale,
    LinearScale,
    PointElement,
    LineElement,
    Title,
    Tooltip,
    Legend
} from 'chart.js'
import { Line } from 'vue-chartjs'
import * as chartConfig from '@/lib/lineChartConfig.js'

ChartJS.register(
    CategoryScale,
    LinearScale,
    PointElement,
    LineElement,
    Title,
    Tooltip,
    Legend
)

const data = chartConfig.data;
const options = chartConfig.options;
const emit = defineEmits(["done"]);

onMounted(() => {
    emit('done')
})

</script>

<template>
    <Line :data="data" :options="options" />
</template>
