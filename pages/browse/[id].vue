<script setup>
const route = useRoute();
</script>
<template>
  <div class="w-full text-center py-10 px-20">
    <h1>Job title:</h1>
    <h2>Job id {{ route.params.id }}</h2>
    <p>The job description is:</p>

    <button class="p-3 bg-slate-800 rounded-lg text-white">Apply</button>

    <p>Company name:</p>
    <p>Location:</p>

    <h3>Position:</h3>
    <p>Position location:</p>
    <p>Salary</p>

    <h3>Posted date:</h3>
  </div>
</template>

<style scoped></style>
