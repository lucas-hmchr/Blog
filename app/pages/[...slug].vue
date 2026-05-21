<script setup lang="ts">
const route = useRoute()

const { data: post } = await useAsyncData('blog-post-' + route.path, () => {
  return queryCollection('content').path(route.path).first()
})

if (!post.value) {
  throw createError({ statusCode: 404, statusMessage: 'post not found', fatal: true })
}
</script>

<template>
  <article class="mx-auto max-w-3xl">
    <NuxtLink
        to="/blog"
        class="text-sm text-cyan-400 transition hover:text-cyan-300"
    >
      ← Zurück zum Blog
    </NuxtLink>

    <header class="mt-8 border-b border-zinc-800 pb-8">
      <p v-if="post!.date" class="text-sm text-zinc-500">
        {{ post!.date }}
      </p>

      <h1 class="mt-3 text-4xl font-bold tracking-tight">
        {{ post!.title }}
      </h1>

      <p class="mt-4 text-lg leading-8 text-zinc-400">
        {{ post!.description }}
      </p>
    </header>

    <ContentRenderer
        v-if="post"
        :value="post"
        class="content-prose mt-8"
    />
  </article>
</template>
