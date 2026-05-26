<script setup lang="ts">
import BlogCard from "~/components/BlogCard.vue";

const {data: posts} = await useAsyncData('blog-posts', () => {
  return queryCollection('content')
      .order('date', 'DESC')
      .all()
})

const {data: postCountAll} = await useAsyncData('blog-post-count', () => {
  return queryCollection('content').count()
})

const postCount = computed(() => {
  if (filteredPosts.value) {
    return filteredPosts.value.length
  } else {
    return postCountAll.value
  }
})

const tagList = computed(() => {
  const tagSet = new Set<string>()
  for (const post of posts.value ?? []) {
    for (const tag of post.tags!)
      tagSet.add(tag)
  }
  return tagSet
})

const selectedTag = ref<null | string>(null)

const selectTag = (tag: string) => {
  if (selectedTag.value === tag) {
    selectedTag.value = null
  } else {
    selectedTag.value = tag
  }
}

const filteredPosts = computed(() => {
  let result = posts.value ?? []
  if (selectedTag.value) {
    result = result.filter(post => post.tags?.includes(selectedTag.value!))
  }
  if (searchQuery.value) {
    result = result.filter(post => hasSearchQuery(post))
  }
  return result
})

const hasSearchQuery = (post: any) => {
  return (
      post.title.toLowerCase().includes(searchQuery.value.toLowerCase()) ||
      post.description.toLowerCase().includes(searchQuery.value.toLowerCase()) ||
      post.tags?.some(tag => tag.toLowerCase().includes(searchQuery.value.toLowerCase()))
  )
}

const searchQuery = ref('')

const resetFilter = () => {
  selectedTag.value = null
  searchQuery.value = ''
}

const hasActiveFilter = computed(() => selectedTag.value || searchQuery.value)
</script>

<template>
  <section class="space-y-8">
    <div>
      <h1 class="text-3xl font-bold">Blog</h1>
      <p class="mt-2 text-zinc-400">
        Alle Artikel aus meinem Nuxt Content Blog.
      </p>
      <p><span>{{ postCount }}</span> Beiträge verfügbar</p>
    </div>
    <button v-if="hasActiveFilter" class="border border-white rounded-md px-2 py-1 cursor-pointer"
            @click="resetFilter()">
      Filter zurücksetzen
    </button>
    <div class="flex gap-4 flex-col">
      <span>Nach Suchbegriffen filtern:</span>
      <input v-model="searchQuery" type="text" placeholder="Suche..."
             class="border border-white rounded-md px-2 py-1 w-xs">
    </div>

    <div>
      <span>Nach Tags filter:</span>
      <ul class="flex flex-wrap gap-2">
        <li v-for="tag in tagList" :key="tag" @click="selectTag(tag)"
            class="cursor-pointer rounded-full border border-zinc-800 px-3 py-1 text-sm"
            :class="{ 'bg-zinc-800': selectedTag === tag }">
          {{ tag }}
        </li>
      </ul>
    </div>

    <div class="grid gap-4">
      <BlogCard
          v-for="post in filteredPosts"
          :key="post.path"
          :post="post"
      />
    </div>
  </section>
</template>