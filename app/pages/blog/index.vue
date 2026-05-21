<script setup lang="ts">
import BlogCard from "~/components/BlogCard.vue";

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
      <BlogCard
          v-for="post in posts"
          :key="post.path"
          :post="post"
      />
    </div>
  </section>
</template>