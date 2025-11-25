<script setup>
import { RouterView } from 'vue-router'
</script>

<template>
  <main style="padding: 1.5rem; font-family: system-ui, sans-serif">
    <RouterView />
  </main>
</template>

<style scoped>
main {
  max-width: 600px;
  margin: 0 auto;
}
</style>
