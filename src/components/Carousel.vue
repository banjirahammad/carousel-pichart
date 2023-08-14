<script setup>
import {
    ref,
    onMounted,
    onBeforeUnmount,
    nextTick
} from 'vue';

let carousel = null

const items = ref([
    
    'https://images.unsplash.com/photo-1636484807469-e33af13716b7?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1yZWxhdGVkfDF8fHxlbnwwfHx8fHw%3D&auto=format&fit=crop&w=1650&q=80',
    'https://images.unsplash.com/photo-1614082242765-7c98ca0f3df3?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1650&q=80',
    'https://images.unsplash.com/photo-1645447556627-137df9819feb?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1yZWxhdGVkfDV8fHxlbnwwfHx8fHw%3D&auto=format&fit=crop&w=1650&q=80',
    'https://images.unsplash.com/photo-1566323526101-051f07ee8925?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1yZWxhdGVkfDEzfHx8ZW58MHx8fHx8&auto=format&fit=crop&w=1650&q=80',
    
])

onMounted(() => {
    carousel = new Flickity('#carousel', {
        autoPlay: 1500,
        wrapAround: true
    })
})

onBeforeUnmount(() => {
    carousel.destroy()
    // carousel = null
    // carousel.destroy()
})

let newItem = ref('')

function addCarouselItem() {
    carousel.destroy()
    items.value.push(newItem.value)

    nextTick(() => {
        carousel = new Flickity('#carousel', {
            autoPlay: 1500,
            wrapAround: true
        })
    })
}
</script>

<template>
    <section class="w-full ">
        <div class="container  bg-gradient-to-r from-red-200 via-red-300 to-yellow-200 rounded-3xl m-10 p-10">
            <h2 class="text-center font-bold text-5xl">Carousel</h2>
            <form class="mt-5 ">
                <div class="flex place-content-center gap-6 mb-6 grid-cols-2">
                    <div>
                        <input v-model="newItem" type="url"
                            class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500 w-[300px]"
                            required placeholder="Give an Image URL">
                    </div>

                    <div>
                        <button @click.prevent="addCarouselItem()" type="submit"
                            class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm w-full sm:w-auto px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800">Add
                            New Carousel</button>
                    </div>
                </div>
            </form>
            <div class="container items mx-auto mt-3" id="carousel">
                <div :style="`background-image:url(${item})`" class="item rounded" v-for="(item, index) in items" :key="item">
                </div>
            </div>
        </div>
    </section>
</template>

<style scoped>
.items {
    width: 1000px;
    height: 400px;
}

.item {
    width: 1000px;
    height: 400px;
    background-color: gray;
    background-size: cover;
    background-position: center;
}
</style>