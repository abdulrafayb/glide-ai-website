<script setup lang="ts">
import gsap from 'gsap';
import type { Content } from '@prismicio/client';

// The array passed to `getSliceComponentProps` is purely optional.
// Consider it as a visual hint for you when templating your slice.
defineProps(
  getSliceComponentProps<Content.HeroSlice>([
    'slice',
    'index',
    'slices',
    'context',
  ])
);

onMounted(() => {
  const preferReducedMotion = window.matchMedia(
    '(prefers-reduced-motion: reduce)'
  ).matches;

  if (preferReducedMotion) {
    // removing animations for accessibility
    return;
  }

  const tl = gsap.timeline({ defaults: { ease: 'power2.inOut' } });

  tl.fromTo(
    '.hero_heading',
    { scale: 0.5, opacity: 0 },
    { scale: 1, opacity: 1, duration: 1.4 }
  );
  tl.fromTo(
    '.hero_body',
    { y: 20, opacity: 0 },
    { y: 0, opacity: 1, duration: 1.2 },
    '-=0.6'
  );
  tl.fromTo(
    '.hero_cta',
    { scale: 1.5, opacity: 0 },
    { scale: 1, opacity: 1, duration: 1.3 },
    '-=0.8'
  );
  tl.fromTo(
    '.hero_image',
    { y: 100, opacity: 0 },
    { y: 0, opacity: 1, duration: 1.1 },
    '+=0.3'
  );
  tl.fromTo(
    '.hero_glow',
    { scale: 0.5, opacity: 0 },
    { scale: 1, opacity: 1, duration: 1.8 },
    '+=1'
  );

  tl.to('.hero_glow_one', {
    ease: 'power2.inOut',
    repeat: -1,
    repeatDelay: 0,
    keyframes: [
      { top: '0%', left: '33%', duration: 0 },
      { top: '33%', left: '33%', duration: 2 },
      { top: '33%', left: '0%', duration: 3 },
      { top: '0%', left: '0%', duration: 2 },
      { top: '0%', left: '33%', duration: 3 },
    ],
  });
  tl.to('.hero_glow_two', {
    ease: 'power2.inOut',
    repeat: -1,
    repeatDelay: 0,
    keyframes: [
      { top: '33%', left: '0%', duration: 0 },
      { top: '0%', left: '0%', duration: 2 },
      { top: '0%', left: '33%', duration: 3 },
      { top: '33%', left: '33%', duration: 2 },
      { top: '33%', left: '0%', duration: 3 },
    ],
  });
});
</script>

<template>
  <Bounded
    :data-slice-type="slice.slice_type"
    :data-slice-variation="slice.variation"
  >
    <div class="text-center relative">
      <GlideGrid />
      <PrismicText
        :field="slice.primary.heading"
        wrapper="h1"
        class="hero_heading mx-auto max-w-3xl text-balance text-5xl md:text-7xl font-medium"
      />
      <PrismicText
        :field="slice.primary.body"
        wrapper="p"
        class="hero_body mx-auto mt-6 max-w-md text-balance text-gray-300"
      />
      <div class="flex flex-wrap gap-8 justify-center mt-8">
        <PrismicLink
          v-for="cta in slice.primary.ctas"
          :key="cta.key"
          :field="cta"
          class="hero_cta buttonLink"
        />
      </div>
      <div class="hero_image glassContainer mt-16 w-fit">
        <div
          class="hero_glow hero_glow_one absolute left-1/3 top-0 -z-10 h-2/3 w-2/3 bg-sky-700/50 blur-3xl md:blur-[120px] filter mix-blend-screen"
        />
        <div
          class="hero_glow hero_glow_two absolute left-0 top-1/3 -z-10 h-2/3 w-2/3 bg-teal-600/50 blur-3xl md:blur-[120px] filter mix-blend-screen"
        />
        <PrismicImage :field="slice.primary.image" class="rounded-lg" />
      </div>
    </div>
  </Bounded>
</template>
