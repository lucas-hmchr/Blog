<script setup lang="ts">
type ButtonVariant = 'primary' | 'secondary' | 'ghost'
type ButtonSize = 'sm' | 'md' | 'lg'

const props = withDefaults(defineProps<{
  to?: string
  variant?: ButtonVariant
  size?: ButtonSize
}>(), {
  to: '/',
  variant: 'primary',
  size: 'md',
})

const baseClasses = [
  'inline-flex',
  'items-center',
  'justify-center',
  'rounded-xl',
  'border-2',
  'font-medium',
  'transition',
  'focus-visible:outline-none',
  'focus-visible:ring-2',
  'focus-visible:ring-cyan-400',
  'focus-visible:ring-offset-2',
  'focus-visible:ring-offset-zinc-950',
]

const variants: Record<ButtonVariant, string> = {
  primary: 'border-cyan-400 bg-cyan-400 text-zinc-950 hover:bg-transparent hover:text-cyan-400',
  secondary: 'border-cyan-400 bg-transparent text-cyan-400 hover:bg-cyan-400 hover:text-zinc-950',
  ghost: 'border-transparent bg-transparent text-zinc-400 hover:text-cyan-400',
}

const sizes: Record<ButtonSize, string> = {
  sm: 'px-4 py-2 text-sm',
  md: 'px-5 py-3 text-base',
  lg: 'px-6 py-4 text-lg',
}
</script>

<template>
  <NuxtLink
      :to="props.to"
      :class="[
      baseClasses,
      variants[props.variant],
      sizes[props.size]
    ]"
  >
    <slot />
  </NuxtLink>
</template>