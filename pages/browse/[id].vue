<script setup>
const route = useRoute();

const { data: job } = await useFetch(
  `http://127.0.0.1:8000/api/v1/jobs/${route.params.id}/`
);
</script>
<template>
  <div class="w-full text-center py-10 px-20">
    <h1>Job title: {{ job.title }}</h1>
    <h2>Job id {{ job.id }}</h2>
    <p>The job description is: {{ job.description }}</p>

    <button class="p-3 bg-slate-800 rounded-lg text-white">Apply</button>

    <p>Company name: {{ job.company_email }}</p>
    <p>Location: {{ job.position_location }}</p>

    <p>Position location: {{ job.position_location }}</p>
    <p>Salary: {{ job.position_salary }}</p>

    <h3>Posted date: {{ job.created_at_formatted }}</h3>
  </div>
</template>

<style scoped></style>
