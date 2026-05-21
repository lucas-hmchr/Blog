<script setup lang="ts">
defineProps<{
  post: {
    path: string
    title?: string
    description?: string
    date?: string
  }
}>()
</script>

<template>
  <NuxtLink
      :to="post.path"
      class="group rounded-2xl border border-zinc-800 bg-zinc-900/60 p-5 transition hover:border-cyan-400 hover:bg-zinc-900"
  >
    <p v-if="post.date" class="text-sm text-zinc-500">
      {{ post.date }}
    </p>

    <h2 class="mt-2 text-xl font-semibold group-hover:text-cyan-300">
      {{ post.title }}
    </h2>

    <p class="mt-2 text-zinc-400">
      {{ post.description }}
    </p>
  </NuxtLink>
</template>