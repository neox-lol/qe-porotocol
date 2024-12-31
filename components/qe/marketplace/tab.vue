<template>
  <div flex-cc>
    <nav class="divide-x rounded-lg flex-cc divide-x-2 divide-gray-6 shadow isolate" aria-label="Tabs">
      <a v-for="(tab, tabIdx) in tabs" :key="tab.name" :href="tab.href" :class="[tab.current ? 'text-gray-300 bg-gray-9' : 'text-gray-400 bg-gray-7 hover:text-gray-2', tabIdx === 0 ? 'rounded-l-lg' : '', tabIdx === tabs.length - 1 ? 'rounded-r-lg' : '', 'group relative  min-w-20 sm:min-w-50 overflow-hidden  py-4 px-4 text-center text-sm font-medium hover:bg-gray-9 focus:z-10']" :aria-current="tab.current ? 'page' : undefined">
        <span>{{ tab.name }}</span>
        <span aria-hidden="true" :class="[tab.current ? 'bg-lime-500' : 'bg-transparent', 'absolute inset-x-0 bottom-0 h-0.5']" />
      </a>
    </nav>
  </div>
</template>

<script setup>
const tabs = [
  { name: 'All', href: '#', current: true },
  { name: 'Ask', href: '#', current: false },
  { name: 'Bid', href: '#', current: false },
]
</script>