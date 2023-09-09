<script setup lang="ts"></script>
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
