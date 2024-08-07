<script setup>
import Cards from "./components/Cards.vue";
import { ref, onMounted } from 'vue'

let userData = ref([]);
let limit = ref(3);

const handleData = () => {
    // console.log(window.innerHeight);
    // console.log(document.documentElement.scrollTop);
    // console.log(document.documentElement.scrollHeight);

    let innerHeight = window.innerHeight;
    let scrollTop = document.documentElement.scrollTop;
    let scrollHeight = document.documentElement.scrollHeight;

    if (innerHeight + scrollTop + 1 >= scrollHeight) {
        limit.value += 3;
    }
}


onMounted(async () => {
    const res = await fetch('https://jsonplaceholder.typicode.com/users');
    const data = await res.json();

    // console.log(data)
    userData.value = data;
})

onMounted(() => {
    window.addEventListener("scroll", handleData);
})
</script>

<template>
    <h1 class="text-3xl font-bold text-center my-5">Infinite Scroll</h1>

    <div class="grid p-5 md:grid-col-3 gap-4">
        <Cards v-for="data in userData.slice(0, limit)" :key="data.id" :data="data" />
    </div>
</template>