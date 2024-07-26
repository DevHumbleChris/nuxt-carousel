<script setup lang="ts">
useHead({
  meta: [
    { property: "og:title", content: `Nuxt Carousel` },
    {
      name: "description",
      content: "Simple Carousel in Nuxt app with little animations.",
    },
    {
      property: "og:description",
      content: "Simple Carousel in Nuxt app with little animations.",
    },
    { property: "og:url", content: "https://admin.kreativestores.com" },
    { name: "twitter:title", content: "Nuxt Carousel" },
    {
      name: "twitter:description",
      content: "Simple Carousel in Nuxt app with little animations.",
    },
    { name: "twitter:site", content: "https://admin.kreativestores.com" },
  ],
  title: `Nuxt Carousel`,
});
</script>

<template>
  <main>
    <slot />
  </main>
</template>
