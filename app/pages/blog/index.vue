<script setup lang="ts">
const { data: posts } = await useAsyncData('blog-posts', () => {
  return queryCollection('content')
      .order('date', 'DESC')
      .all()
})
</script>

<template>
  <section class="space-y-8">
    <div>
      <h1 class="text-3xl font-bold">Blog</h1>
      <p class="mt-2 text-zinc-400">
        Alle Artikel aus meinem Nuxt Content Blog.
      </p>
    </div>

    <div class="grid gap-4">
      <NuxtLink
          v-for="post in posts"
          :key="post.path"
          :to="post.path"
          class="rounded-2xl border border-zinc-800 bg-zinc-900/60 p-5 transition hover:border-cyan-400"
      >
        <p class="text-sm text-zinc-500">
          {{ post.date }}
        </p>

        <h2 class="mt-2 text-xl font-semibold">
          {{ post.title }}
        </h2>

        <p class="mt-2 text-zinc-400">
          {{ post.description }}
        </p>
      </NuxtLink>
    </div>
  </section>
</template>