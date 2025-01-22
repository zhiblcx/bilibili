<script setup lang="ts">
import { useRoute } from '#app'
const route = useRoute()
</script>

<template>
  <NuxtLayout name="home-layouts" />
  {{ route.params.id }}
</template>

<style scoped></style>
