<script setup>
// Categories
let { data: jobCategories } = await useFetch(
  `http://127.0.0.1:8000/api/v1/jobs/categories/`
);
let selectedCategory = ref("");
let selectedCategories = [];
let searchText = ref("");

const toggleCategory = (id) => {
  const index = selectedCategories.indexOf(id); // check if id is already selected
  console.log(index, id);

  if (index === -1) {
    selectedCategories.push(id);
  } else {
    selectedCategories.splice(index, 1);
  }

  selectedCategory.value = selectedCategories.join(",");
};

let { data: jobs } = await useFetch("http://127.0.0.1:8000/api/v1/jobs/", {
  query: { searchText: searchText, categories: selectedCategory },
});

// search functionality
const handleSearch = () => {
  const oldSearchText = searchText.value;
  searchText.value = "";
  searchText.value = oldSearchText;
};
</script>
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
            v-model="searchText"
            type="text"
            id="searchBar"
            placeholder="Find a job"
            class="rounded-l-lg pl-2 outline-none"
          />
          <button class="p-3 bg-slate-950 rounded-lg" @click="handleSearch">
            <BaseIconSearch class="w-6 h-6 text-white" />
          </button>
        </div>

        <div class="jobCategory text-white pt-4">
          <h2 class="border-b-2 border-gray-400 mb-2">Categories</h2>
          <div v-for="category in jobCategories" :key="category.id">
            <p
              @click="toggleCategory(category.id)"
              class="cursor-pointer py-2"
              :class="{
                'bg-slate-600 rounded-lg px-1 my-1': selectedCategory.includes(
                  category.id
                ),
              }"
            >
              {{ category.title }}
            </p>
          </div>
        </div>
      </div>

      <div class="jobTable px-5 space-y-3 w-4/5">
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
