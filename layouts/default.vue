<script setup>
import { useUserStore } from "~/stores/user";

const userStore = useUserStore();
const route = useRoute();
const router = useRouter();

onMounted(() => {
  userStore.initStore();
  if (route.fullPath.includes("/auth")) {
    setTimeout(() => {
      router.push("/");
    }, 500);
  }
});
</script>
<template>
  <div>
    <SharedHeader />
    <div role="main" class="min-h-[calc(100vh-148px)]">
      <slot />
    </div>
    <SharedFooter />
  </div>
</template>

<style>
@import "~/assets/scss/default.scss";
</style>
