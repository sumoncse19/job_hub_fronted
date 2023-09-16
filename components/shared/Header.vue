<script setup>
import { useUserStore } from "~/stores/user";

const router = useRouter();
const userStore = useUserStore();

const handleLogOut = () => {
  userStore.removeToken();
  router.push("/");
  console.log("from handle log out");
};
</script>
<template>
  <nav class="flex justify-between items-center p-6 bg-slate-700 text-white">
    <NuxtLink to="/" class="font-bold text-2xl">Job Hub</NuxtLink>

    <div class="flex justify-center items-center space-x-3 font-bold text-lg">
      <NuxtLink to="/" class="">Home</NuxtLink>
      <NuxtLink to="/browse" class="">Browse</NuxtLink>

      <div v-if="userStore.user.isAuthenticated" class="flex space-x-3">
        <NuxtLink to="/myjobs" class="bg-amber-700 p-2 rounded-lg"
          >My Jobs</NuxtLink
        >
        <NuxtLink to="/createjob" class="bg-green-700 p-2 rounded-lg"
          >Create Job</NuxtLink
        >
        <button @click="handleLogOut" class="bg-green-700 p-2 rounded-lg">
          Log Out
        </button>
      </div>

      <div v-else class="flex space-x-3">
        <NuxtLink to="/auth/register" class="bg-amber-700 p-2 rounded-lg"
          >Sign Up</NuxtLink
        >
        <NuxtLink to="/auth/login" class="bg-green-700 p-2 rounded-lg"
          >Login</NuxtLink
        >
      </div>
    </div>
  </nav>
</template>

<style scoped></style>
