<script setup>
const route = useRoute();
</script>
<template>
  <nav class="flex justify-between items-center p-6 bg-slate-700 text-white">
    <NuxtLink to="/" class="font-bold text-2xl">Job Hub</NuxtLink>

    <div class="flex justify-center items-center space-x-3 font-bold text-lg">
      <NuxtLink to="/" class="">Home</NuxtLink>
      <NuxtLink to="/browse" class="">Browse</NuxtLink>

      <div v-if="!route.fullPath.includes('/auth/')" class="flex space-x-3">
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
