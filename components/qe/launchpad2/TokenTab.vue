<template>
  <div class="border-b border-gray-5">
    <nav class="flex -mb-px space-x-8" aria-label="Tabs">
      <a v-for="tab in tabs" :key="tab.name" :href="tab.href" :class="[tab.current ? 'border-gray-3 text-gray-3' : 'border-transparent text-gray-5 hover:border-gray-300 hover:text-gray-3', 'whitespace-nowrap border-b-2 py-4 px-1 text-sm font-medium']" :aria-current="tab.current ? 'page' : undefined">{{ tab.name }}</a>
    </nav>
  </div>
</template>

<script setup>
const tabs = [
  { name: 'IXO', href: '#', current: true },
  { name: 'Grid', href: '#', current: false },
  { name: 'Line', href: '#', current: false },
  { name: 'DEX', href: '#', current: false },
]
</script>