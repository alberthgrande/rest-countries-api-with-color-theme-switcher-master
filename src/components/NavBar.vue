<template>
  <div class="p-8">
    <nav class="flex justify-between">
      <h1>Where in the world?</h1>
      <button @click="toggleDark()">Dark Mode</button>
    </nav>
  </div>
</template>
<script setup>
import { useDark, useToggle } from "@vueuse/core";

const isDark = useDark();
const toggleDark = useToggle(isDark);
</script>
<style>
.dark {
  background: #242424;
  color: #fff;
}
</style>
