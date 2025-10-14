<script lang="ts" setup>
import type { Content } from "@prismicio/client";

defineProps<{
  settings?: Content.SettingsDocument;
}>();
</script>

<template>
  <footer>
    <nav
      aria-label="Footer"
      class="flex flex-col justify-between items-center gap-6 py-7 px-8 md:flex-row border-t border-gray-600"
    >
      <NuxtLink to="/">
        <GlideLogo />
        <span class="sr-only">{{ settings?.data.site_title }} home page</span>
      </NuxtLink>

      <ul class="flex gap-6">
        <li v-for="link in settings?.data.navigation" :key="link.key">
          <PrismicLink
            class="inline-flex items-center min-h-11"
            :field="link"
          />
        </li>
      </ul>
    </nav>
  </footer>
</template>
