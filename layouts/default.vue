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
  link: [{ rel: "icon", href: "/icon.png" }],
});

useSeoMeta({
  viewport: "width=device-width, initial-scale=1, maximum-scale=1",
  title: "Nuxt Carousel",
  description: "Simple Carousel in Nuxt app with little animations.",
  ogImage: "/social-image.png",
  twitterImage: "/social-image.png",
  twitterCard: "summary_large_image",
});
</script>

<template>
  <main>
    <slot />
  </main>
</template>
