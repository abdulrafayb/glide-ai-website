<script lang="ts" setup>
import type { Content } from "@prismicio/client";

defineProps<{
  settings?: Content.SettingsDocument;
}>();

const isOpen = ref(false);
</script>

<template>
  <header class="p-4 md:p-6">
    <nav
      aria-label="Main"
      class="mx-auto max-w-6xl flex flex-col justify-between py-2 md:flex-row md:items-center"
    >
      <div class="flex justify-between items-center">
        <NuxtLink to="/" class="z-50" @click="isOpen = false">
          <GlideLogo />
          <span class="sr-only">{{ settings?.data.site_title }} home page</span>
        </NuxtLink>
        <button
          class="flex items-center md:hidden p-2 text-3xl"
          :aria-expanded="isOpen"
          @click="isOpen = true"
        >
          <Icon name="ph:list-bold" />
        </button>
      </div>

      <ul class="hidden md:flex gap-6">
        <li v-for="link in settings?.data.navigation" :key="link.key">
          <PrismicLink
            class="inline-flex items-center min-h-11"
            :field="link"
            :class="{ buttonLink: link.variant === 'Button' }"
          />
        </li>
      </ul>

      <!-- Mobile Nav -->
      <div
        class="md:hidden fixed inset-0 z-40 flex flex-col items-end bg-gray-950 pr-4 pt-6 transition-transform duration-300 ease-in-out will-change-transform"
        :class="isOpen ? 'translate-x-0' : 'translate-x-full'"
      >
        <button class="flex items-center p-2 text-3xl" @click="isOpen = false">
          <Icon name="ph:x-bold" />
        </button>
        <ul class="grid justify-items-end gap-6">
          <li
            v-for="link in settings?.data.navigation"
            :key="link.key"
            class="first:mt-8"
          >
            <PrismicLink
              class="block min-h-11 px-3 text-3xl"
              :field="link"
              :class="{ buttonLink: link.variant === 'Button' }"
            />
          </li>
        </ul>
      </div>
    </nav>
  </header>
</template>
