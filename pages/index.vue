<script setup lang="ts">
import { Button } from "~/components/ui/button";
import { cn } from "~/lib/utils";

const images_data = ref([
  {
    id: 1,
    src: "/images/axelf-cop.jpg",
    name: "Beverly Hills Cop: Axel F",
    info: "Forty years after his unforgettable first case in Beverly Hills, Detroit cop Axel Foley returns to do what he does best: solve crimes and cause chaos.",
  },
  {
    id: 2,
    src: "/images/bad-boys.jpg",
    name: "Bad Boys: Ride or Die",
    info: "After their late former Captain is framed, Lowrey and Burnett try to clear his name, only to end up on the run themselves.",
  },
  {
    id: 3,
    src: "/images/migration.jpg",
    name: "Migration",
    info: "After a migrating duck family alights on their pond with thrilling tales of far-flung places, the Mallard family embarks on a family road trip, from New England, to New York City, to tropical Jamaica.",
  },
  {
    id: 4,
    src: "/images/quiet-place.jpg",
    name: "A Quiet Place: Day One",
    info: "As New York City is invaded by alien creatures who hunt by sound, a woman named Sam fights to survive with her cat.",
  },
  {
    id: 5,
    src: "/images/the-boys.jpg",
    name: "The Boys",
    info: "A group of vigilantes known informally as “The Boys” set out to take down corrupt superheroes with no more than blue-collar grit and a willingness to fight dirty.",
  },
  {
    id: 6,
    src: "/images/wolverine.jpg",
    name: "Deadpool & Wolverine",
    info: "A listless Wade Wilson toils away in civilian life with his days as the morally flexible mercenary, Deadpool, behind him. But when his homeworld faces an existential threat, Wade must reluctantly suit-up again with an even more reluctant Wolverine.",
  },
]);

const images = ref(images_data);
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
  <div>
    <h1 class="text-3xl font-bold text-center mt-[3.5rem]">Nuxt Carousel</h1>
    <div
      class="relative h-96 w-full lg:w-[90%] mx-auto items-center flex justify-center overflow-hidden -z-10 -mt-[2rem]"
    >
      <div
        v-for="(image, i) in images"
        :key="image.id"
        :class="
          cn(
            'rounded-3xl overflow-hidden h-60 border border-neutral-200 dark:border-neutral-700 shadow-md mx-1 relative',
            getPosition(i) === currentIndex
              ? 'flex-none aspect-[8/6] lg:aspect-[5/2] transition-all duration-700 relative'
              : 'aspect-[1/6] lg:aspect-[1/6] flex-shrink-0'
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
        <NuxtImg
          :src="image.src"
          class="h-full w-full object-cover"
          :alt="`Carousel image ${i + 1}`"
          :class="
            getPosition(i) === currentIndex &&
            'transition duration-700 ease-in-out'
          "
        />
        <div
          v-if="getPosition(i) === currentIndex"
          class="absolute inset-x-0 bottom-0 h-40 w-full bg-gradient-to-b from-transparent via-black to-black dark:via-black/50 dark:to-black scale-[1.1] pointer-events-none"
        />
        <div
          v-if="getPosition(i) === currentIndex"
          class="absolute bottom-0 inset-x-0 z-10"
        >
          <div class="flex flex-col h-full p-4 sm:p-6">
            <h3
              class="text-lg sm:text-xl font-semibold text-white group-hover:text-white/80 group-focus:text-white/80"
            >
              {{ image.name }}
            </h3>
            <p class="mt-2 text-white/80 text-xs sm:text-sm">
              {{ image.info }}
            </p>
          </div>
        </div>
      </div>
      <button
        @click="handleMove(-1)"
        class="hidden sm:grid h-14 w-14 place-content-center text-3xl transition-colors hover:text-sky-500 absolute -left-6"
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
        class="hidden sm:grid h-14 w-14 place-content-center text-3xl transition-colors hover:text-sky-500 absolute -right-6"
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
    <div class="sm:hidden flex items-center justify-center -mt-[3.5rem]">
      <button
        @click="handleMove(-1)"
        class="grid h-14 w-14 place-content-center text-3xl"
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
        class="grid h-14 w-14 place-content-center text-3xl transition-colors"
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
    <div class="flex items-center justify-center lg:-mt-[3rem] font-bold">
      <NuxtLink
        href="https://github.com/DevHumbleChris/nuxt-carousel"
        target="_blank"
      >
        <Button variant="link"> @thecodingmontana </Button>
      </NuxtLink>
    </div>
  </div>
</template>
