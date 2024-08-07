<script setup>

import Navbar from "./components/Navbar.vue"
import HeroSection from "./components/HeroSection.vue";
import HomeCards from "./components/HomeCards.vue"
import JobLists from "./components/JobLists.vue"
import jobData from "./jobs.json";

</script>

<template>
  <Navbar />
  <HeroSection />
  <HomeCards />
  <JobLists />
</template>
