<script setup>
const { data: jobs } = await useFetch(
  "http://127.0.0.1:8000/api/v1/jobs/newest/"
);
</script>
<template>
  <div class="heroWrap">
    <div
      class="flex flex-col space-y-5 py-16 justify-center items-center bg-gray-600 text-white"
    >
      <h1 class="text-3xl font-bold">Find a job anywhere!</h1>
      <NuxtLink to="/browse" class="p-3 bg-slate-800 rounded-lg"
        >Browse</NuxtLink
      >
    </div>

    <div class="newestJob py-5">
      <h2 class="text-xl font-medium text-center">Newest Jobs</h2>

      <div class="jobTable p-5 space-y-3">
        <div
          v-for="item in jobs"
          :key="item.id"
          class="bg-gray-300 p-5 rounded-xl flex justify-between items-center"
        >
          <div class="flex flex-col">
            <div class="text-lg font-semibold">{{ item.title }}</div>
            <p>{{ item.company_name }}</p>
          </div>
          <div class="flex flex-col">
            <div>{{ item.position_location }}</div>
            <p>${{ item.position_salary }}</p>
          </div>
          <div>Posted {{ item.created_at_formatted }}</div>
          <div class="text-white">
            <NuxtLink
              :to="`/browse/${item.id}`"
              class="p-3 bg-slate-800 rounded-lg"
              >Details</NuxtLink
            >
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped></style>
