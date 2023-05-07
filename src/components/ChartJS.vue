<template>
    <canvas style="width: 100%; height: 100%" ref="chartRef"></canvas>
    <button @click="pause">pause</button>
</template>

<script setup>
import {onMounted, onUnmounted, reactive, ref} from 'vue';
import Chart from 'chart.js/auto';
import 'chartjs-adapter-moment';
import zoomPlugin from 'chartjs-plugin-zoom';
import ChartStreaming from 'chartjs-plugin-streaming';
Chart.register(ChartStreaming);
Chart.register(zoomPlugin);
const _state = reactive({
    pause: false
})
let chartRef = ref(null)
let chart = reactive({});
let data = [
    {
        label: 'CPU',
        fill: false,
        borderColor: 'rgb(195,137,232)',
        borderWidth: 2,
        data: []
    },
    {
        label: 'GPU',
        fill: false,
        borderColor: 'rgb(109,253,154)',
        borderWidth: 2,
        data: []
    }
]
function onRefresh(e) {
    data[0].data.push({ x: Date.now(), y: Math.random()*100})
    data[1].data.push({ x: Date.now(), y: Math.random()*100})
}
function pause() {
    _state.pause = !_state.pause
    chart.options.scales.x.realtime.pause = _state.pause
}


let options =  {
    responsive: true,
    maintainAspectRatio: false,
    elements: {
        point: {
            radius: 3,
        },
    },
    scales: {
        x:{
            // drawTicks: true,
            type: 'realtime',
            display: true,
            realtime: {
                duration: 60000,
                refresh: 1000,
                delay: 1000,
                pause: false,
                onRefresh: onRefresh,
            }
        },
        y: {
            beginAtZero: true,
            min: 0,
            max: 100,
            stepSize: 10
        }
    },
    plugins: {
        streaming: {
            frameRate: 60
        },
        zoom: {
            pan: {
                enabled: true,
                mode: 'x'
            },
            zoom: {
                wheel: {
                    enabled: true,
                },
                pinch: {
                    enabled: true
                },
                mode: 'x'
            }
        }
    }
}
onMounted(() => {
    const ctx = chartRef.value.getContext('2d');
    chart = new Chart(ctx, {
        type: 'line',
        data: {
            datasets: data
        },
        options:options
    });
    // setInterval(() => chart.update(), 1000)
});
onUnmounted(() => {
    chart.destroy();
});

</script>