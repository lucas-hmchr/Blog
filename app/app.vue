<script setup lang="ts">
import AppHeader from "~/components/AppHeader.vue";
</script>

<template>
  <div class="min-h-screen bg-zinc-950 text-zinc-100">
    <AppHeader />

    <main class="mx-auto max-w-4xl px-6 py-10">
      <NuxtPage />
    </main>
  </div>
</template>