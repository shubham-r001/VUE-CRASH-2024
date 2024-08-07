<script setup>
import { defineProps } from "vue";

defineProps({
  backg: {
    type: String,
    default: "bg-gray-100"
  }
})
</script>

<template>
  <div :class="`${backg} p-6 rounded-lg shadow-md`">
    <slot></slot>
  </div>
</template>