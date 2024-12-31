<script setup lang="ts">
import { ChevronLeftIcon, ChevronRightIcon } from "@heroicons/vue/20/solid";

const { pageTitle } = $defineProps<{
  pageTitle: string;
}>();
</script>

<template>
  <nav class="flex" aria-label="Breadcrumb">
    <ol role="list" class="flex space-x-4 items-center">
      <li>
        <div class="flex items-center">
          <NuxtLink to="/grids" class="font-medium text-sm ml-4 text-gray-400 hover:text-gray-200">Grids</NuxtLink>
        </div>
      </li>
      <li>
        <div class="flex items-center">
          <ChevronRightIcon class="flex-shrink-0 h-5 text-gray-500 w-5" aria-hidden="true" />
          <span class="font-medium text-sm ml-4 text-gray-400">{{ pageTitle }}</span>
        </div>
      </li>
    </ol>
  </nav>
</template>
