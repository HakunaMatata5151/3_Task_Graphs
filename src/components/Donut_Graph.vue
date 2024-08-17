<script setup>
import { ref, onMounted } from 'vue';
import { Chart as ChartJS, ArcElement, Tooltip, Legend, } from 'chart.js';
import { Doughnut } from 'vue-chartjs'
import * as chartConfig from '@/lib/dounutChartConfig.js';

ChartJS.register(ArcElement, Tooltip, Legend)

const data = ref(chartConfig.data);
const options = chartConfig.options;

const emit = defineEmits(["done"]);

onMounted(() => {
    emit('done')
})

</script>

<template>
    <div>
        <Doughnut :data="data" :options="options" />
    </div>
</template>

<style scoped></style>
