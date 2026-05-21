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

      <NuxtLink
          to="/blog"
          class="inline-flex rounded-xl bg-cyan-400 px-5 py-3 font-medium text-zinc-950 hover:bg-cyan-300"
      >
        Zum Blog
      </NuxtLink>
    </div>
  </section>
</template>