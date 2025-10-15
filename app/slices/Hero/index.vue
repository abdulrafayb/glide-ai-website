<script setup lang="ts">
import gsap from "gsap";
import type { Content } from "@prismicio/client";

// The array passed to `getSliceComponentProps` is purely optional.
// Consider it as a visual hint for you when templating your slice.
defineProps(
  getSliceComponentProps<Content.HeroSlice>([
    "slice",
    "index",
    "slices",
    "context",
  ])
);
</script>

<template>
  <Bounded
    :data-slice-type="slice.slice_type"
    :data-slice-variation="slice.variation"
  >
    <div class="text-center relative">
      <PrismicText
        :field="slice.primary.heading"
        wrapper="h1"
        class="mx-auto max-w-3xl text-balance text-5xl font-medium"
      />
      <PrismicText
        :field="slice.primary.body"
        wrapper="p"
        class="mx-auto mt-6 max-w-md text-balance text-gray-300"
      />
      <div class="flex flex-wrap gap-8 justify-center mt-8">
        <PrismicLink
          v-for="cta in slice.primary.ctas"
          :key="cta.key"
          :field="cta"
          class="buttonLink"
        />
      </div>
      <div class="glassContainer mt-16 w-fit">
        <div
          class="absolute left-1/3 top-0 -z-10 h-2/3 w-2/3 bg-sky-700/50 blur-3xl md:blur-[120px] filter mix-blend-screen"
        />
        <div
          class="absolute left-0 top-1/3 -z-10 h-2/3 w-2/3 bg-teal-600/50 blur-3xl md:blur-[120px] filter mix-blend-screen"
        />
        <PrismicImage :field="slice.primary.image" />
      </div>
    </div>
  </Bounded>
</template>
