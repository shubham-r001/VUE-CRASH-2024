<script setup>
  import {defineProps} from "vue";


  defineProps({
    title: {
      type: String,
      default:'Become a Frontend Dev'
    },
    subtitle: {
      type: String,
      default:'Find a Frontend Job that match your skill and needs'
    }
  })

</script>

<template>
  <div class="bg-green-800 text-white py-10 text-center h-[20rem] md:h-[25rem] flex flex-col justify-center items-center">
    <h2 class="text-4xl md:text-5xl font-semibold">{{title}}</h2>
    <p class="text-xl text-slate-200 mt-3">{{subtitle}}</p>
  </div>
</template>