<script setup>
import { useUserStore } from "~/stores/user";

const userStore = useUserStore();
const router = useRouter();

const myJobs = ref([]);
const getJobs = async () => {
  await $fetch(`http://127.0.0.1:8000/api/v1/jobs/my-jobs`, {
    headers: {
      Authorization: "token " + userStore.user.token,
      "Content-Type": "application/json",
    },
  })
    .then((response) => {
      myJobs.value = response;
      console.log(myJobs.value, "here ");
    })
    .catch((error) => {
      console.log(error);
    });
};

onMounted(() => {
  if (!userStore.user.isAuthenticated) {
    router.push("/login");
  } else {
    getJobs();
  }
});
</script>
<template>
  <div class="px-6 py-10">
    <h1 class="text-3xl font-bold">My Jobs!</h1>

    <div class="MyJobTable p-5 space-y-3">
      <div
        v-for="item in myJobs"
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
</template>

<style scoped></style>
