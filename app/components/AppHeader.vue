<template>
  <header class="border-b border-zinc-800">
    <nav class="mx-auto flex max-w-4xl items-center justify-between px-6 py-5">
      <NuxtLink to="/" class="text-lg font-bold">
        Mein Blog
      </NuxtLink>

      <div class="flex gap-4 text-sm text-zinc-400">
        <NuxtLink to="/" class="hover:text-white">Home</NuxtLink>
        <NuxtLink to="/blog" class="hover:text-white">Blog</NuxtLink>
      </div>
    </nav>
  </header>
</template>