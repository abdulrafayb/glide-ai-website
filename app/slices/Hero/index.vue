<script setup lang="ts">
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
      <div>
        <PrismicLink
          v-for="link in slice.primary.ctas"
          :key="link.key"
          :field="link"
        />
      </div>
      <PrismicImage :field="slice.primary.image" />
    </div>
  </Bounded>
</template>
