<script setup lang="ts">
const { data: posts } = await useAsyncData('blog-posts', () => {
  return queryCollection('content').limit(3)
      .order('date', 'DESC')
      .all()
})

</script>
<template>
  <section class="space-y-8">
    <div class="space-y-4">
      <p class="text-sm font-medium uppercase tracking-widest text-cyan-400">
        Frontend · Nuxt · Content
      </p>

      <h1 class="text-4xl font-bold tracking-tight sm:text-5xl">
        Ein moderner Blog mit Nuxt Content.
      </h1>

      <p class="max-w-2xl text-lg text-zinc-400">
        Hier schreibe ich über Frontend-Entwicklung, Nuxt, Vue und Dinge,
        die ich beim Bauen lerne.
      </p>

      <BaseButton to="/blog/" variant="primary">
        Zum Blog
      </BaseButton>
    </div>

    <div class="grid gap-4">
      <h2 class="text-3xl">Neuste Beiträge</h2>
      <BlogCard v-for="post in posts" :key="post.id" :post="post" />
    </div>
  </section>
</template>