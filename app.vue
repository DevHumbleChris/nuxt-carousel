<script setup lang="ts">
// import { useMagicKeys } from "@vueuse/core";
import { cn } from "./lib/utils";
const IMAGES_DATA = ref([
  { id: 1, src: "/images/axelf-cop.jpg" },
  { id: 2, src: "/images/bad-boys.jpg" },
  { id: 3, src: "/images/migration.jpg" },
  { id: 4, src: "/images/quiet-place.jpg" },
  { id: 5, src: "/images/the-boys.jpg" },
  { id: 6, src: "/images/wolverine.jpg" },
]);

const images = ref(IMAGES_DATA);
const currentIndex = ref(0);

const { left, right } = useMagicKeys();

watch([left, right], (v) => {
  if (v[0]) {
    handleMove(-1);
  }
  if (v[1]) {
    handleMove(1);
  }
});

const handleMove = (direction: number) => {
  const imgArrCopy = [...images.value];

  if (direction > 0) {
    const firstItem = imgArrCopy.shift();
    if (!firstItem) return;
    imgArrCopy.push({ ...firstItem, id: Math.random() });
  } else {
    const lastItem = imgArrCopy.pop();
    imgArrCopy.unshift({ ...lastItem!, id: Math.random() });
  }

  images.value = imgArrCopy;
};

const getPosition = (index: number) => {
  const length = images.value.length;
  const position = length % 2 ? index - (length + 1) / 2 : index - length / 2;
  return position;
};
</script>

<template>
  <div class="relative h-96 w-[90%] mx-auto items-center flex justify-center">
    <div
      v-for="(image, i) in images"
      :key="image.id"
      :class="
        cn(
          'rounded-3xl overflow-hidden h-60 border border-neutral-200 dark:border-neutral-700 shadow-md mx-1',
          getPosition(i) === currentIndex
            ? 'flex-none aspect-[5/2] transition-all duration-700'
            : 'aspect-[1/6] flex-shrink-0'
        )
      "
      v-motion="{
        initial: {
          opacity: 0,
          scale: 0.5,
        },
        enter: {
          opacity: 1,
          scale: 1,
          transition: {
            type: 'spring',
            stiffness: '100',
            delay: 100,
          },
        },
      }"
    >
      <img
        :src="image.src"
        class="h-full w-full object-cover"
        :alt="`Carousel image ${i + 1}`"
        :class="
          getPosition(i) === currentIndex
            ? 'transition duration-700 ease-in-out'
            : ''
        "
      />
    </div>
    <button
      @click="handleMove(-1)"
      class="grid h-14 w-14 place-content-center text-3xl transition-colors hover:text-sky-500 absolute -left-6"
    >
      <svg
        xmlns="http://www.w3.org/2000/svg"
        fill="none"
        viewBox="0 0 24 24"
        strokeWidth="{1.5}"
        stroke="currentColor"
        class="w-6 h-6"
      >
        <path
          strokeLinecap="round"
          strokeLinejoin="round"
          d="M15.75 19.5 8.25 12l7.5-7.5"
        />
      </svg>
    </button>
    <button
      @click="handleMove(1)"
      class="grid h-14 w-14 place-content-center text-3xl transition-colors hover:text-sky-500 absolute -right-6"
    >
      <svg
        xmlns="http://www.w3.org/2000/svg"
        fill="none"
        viewBox="0 0 24 24"
        strokeWidth="{1.5}"
        stroke="currentColor"
        class="w-6 h-6"
      >
        <path
          strokeLinecap="round"
          strokeLinejoin="round"
          d="m8.25 4.5 7.5 7.5-7.5 7.5"
        />
      </svg>
    </button>
  </div>
</template>
