<script setup>
import { ref } from "vue";
import jobData from "../jobs.json";
import JobCard from "./JobCard.vue";

const jobs = ref(jobData);
</script>

<template>
    <section class="bg-green-50 px-4 py-10">
        <div class="max-w-7xl m-auto">
            <h2 class="text-3xl font-bold text-green-500 mb-6 text-center">
                Browse Jobs
            </h2>
            <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
                <JobCard v-for="job in jobs" :key="job.id" :job="job" />
            </div>
        </div>
    </section>
</template>