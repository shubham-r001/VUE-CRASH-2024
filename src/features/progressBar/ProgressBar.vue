<script setup>
import { ref, onMounted, reactive } from "vue";


let width = ref(0);
let themeChange = ref(false);
const isWidthExceed = width.value > 50;

const updateWidthValue = () => {
    let time;
    let timer = setInterval(() => {
        // console.log(Math.round(Math.random() * (taskTimer.length - 1)))
        if (width.value >= 100) clearInterval(timer)
        else {
            width.value += 1;
        }
    }, 100);
}

const styleObject = reactive({
    width: `${width}%`,
})

const toggleTheme = () => {
    themeChange.value = !themeChange.value;
}

onMounted(() => {
    // fn to generate progress counter running
    updateWidthValue();
})

</script>

<template>
    <div class="relative m-10">
        <div class="bg-green-500 w-full h-8 rounded-xl flex justify-center items-center">
            <span class="z-10">{{ width }}%</span>
        </div>
        <div :style="{ 'width': width + '%' }"
            class=" bg-purple-500 h-8 rounded-xl flex justify-center items-center absolute top-0 left-0"
            :class="{ active: themeChange }">
        </div>
    </div>

    <button @click="toggleTheme">Change Theme</button>
</template>

<style scoped>
.active {
    background-color: blue;
}
</style>