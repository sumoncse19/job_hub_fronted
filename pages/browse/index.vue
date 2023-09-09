<script setup lang="ts"></script>
<template>
  <div class="browseWrap px-10">
    <h2 class="text-xl font-medium text-center my-10">
      Browse your desire jobs!
    </h2>
    <div class="flex space-x-3 w-full">
      <div
        class="bg-slate-800 h-fit min-w-[285px] max-w-1/5 flex flex-col justify-center rounded-lg p-4"
      >
        <div class="searchBar flex rounded-lg">
          <input
            type="text"
            id="searchBar"
            placeholder="Find a job"
            class="rounded-l-lg pl-2 outline-none"
          />
          <button class="p-3 bg-slate-950 rounded-lg">
            <BaseIconSearch class="w-6 h-6 text-white" />
          </button>
        </div>

        <div class="jobCategory text-white pt-4">
          <h2 class="border-b-2 border-gray-400 mb-2">Categories</h2>
          <div v-for="(category, index) in 5" :key="index">
            Category {{ index }}
          </div>
        </div>
      </div>

      <div class="jobTable px-5 space-y-3 w-4/5">
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
