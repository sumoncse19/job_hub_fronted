<script setup lang="ts"></script>
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
          v-for="(item, index) in 5"
          :key="index"
          class="bg-gray-300 p-5 rounded-xl flex justify-between items-center"
        >
          <div class="flex flex-col">
            <div class="text-lg font-semibold">The Job Position</div>
            <p>The company name</p>
          </div>
          <div class="flex flex-col">
            <div>World wide</div>
            <p>$90-120k</p>
          </div>
          <div>Posted Dec. 1, 2022</div>
          <div class="text-white">
            <NuxtLink
              :to="`/browse/${index + 1}`"
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
