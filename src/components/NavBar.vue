<template>
  <div class="py-8">
    <nav class="flex justify-between border-b p-4">
      <h1>Where in the world?</h1>
      <button @click="toggleDark()">Dark Mode</button>
    </nav>
  </div>
</template>

<script setup>
import { useDark, useToggle } from "@vueuse/core";

// Use VueUse to handle dark mode
const isDark = useDark();
const toggleDark = useToggle(isDark);
</script>

<style scoped>
/* Light mode navbar border-bottom */
nav {
  border-bottom: 1px solid #ddd; /* Light gray border for light mode */
}

/* Dark mode navbar border-bottom */
.dark nav {
  border-bottom: 1px solid #555; /* Darker border for dark mode */
}
</style>
