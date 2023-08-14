<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue';
const newItem = ref(16)

let pieChart = null

const dataset = [
    300, 50, 100
]

const data = {
    labels: [
        'Red',
        'Blue',
        'Yellow'
    ],
    datasets: [{
        label: 'My First Dataset',
        data: dataset,
        backgroundColor: [
            'rgb(255, 99, 132)',
            'rgb(54, 162, 235)',
            'rgb(255, 205, 86)',
            'rgb(43, 105, 86)',
            'rgb(21, 21, 186)',
        ],
        hoverOffset: 4
    }]
};

const config = {
    type: 'pie',
    data: data,
};

onMounted(() => {
    const ctx = document.getElementById('chart')
    pieChart = new Chart(ctx, config)
})

onBeforeUnmount(() => {
    pieChart.destroy()
})

function updateChart() {
    dataset.push(newItem.value)
    pieChart.data.datasets[0].data = dataset
    pieChart.update()
}

</script>

<template>
    <section
        class=" container bg-[conic-gradient(at_bottom_left,_var(--tw-gradient-stops))] from-fuchsia-300 via-green-400 to-rose-700 rounded-3xl m-10 p-10">

        <h2 class="text-center font-bold text-5xl mb-4">Pie-Chart</h2>
        <div class=" mx-auto w-[400px] h-[400px] bg-gray-400 rounded">
            <canvas id="chart">
            </canvas>
        </div>

        <div class="mt-10 flex place-content-center gap-5 mb-6 grid-cols-2">
            <input type="text"
                class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500 w-[250px]"
                v-model="newItem">
            <button @click="updateChart()"
                class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm w-full sm:w-auto px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800">
                Add
            </button>

        </div>
    </section>
</template>

<style scoped></style>
