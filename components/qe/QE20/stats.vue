<template>
  <div class="rounded-xl bg-gray-900 overflow-hidden">
    <div class="mx-auto max-w-7xl">
      <div class="bg-white/5 gap-px grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3">
        <div v-for="(stat, index) in stats" :key="stat.name" class="bg-gray-900 py-6 px-4 sm:px-6 lg:px-8">
          <p class="font-medium text-sm text-gray-400 leading-6">{{ stat.name }}</p>
          <p class="flex mt-2 gap-x-2 items-center justify-between">
            <span class="font-semibold text-white tracking-tight text-4xl">{{ stat.value }} {{ stat.unit }}</span>
            <BsBtnBlack bg-rainbow class="animate-pulse" v-if="index == 2">Buy $QE</BsBtnBlack>
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
const stats = [
  { name: 'Your Rank', value: '# 123', unit: '' },
  { name: 'You have invited', value: '10', unit: 'Users' },
  { name: 'You owned $QE', value: '234', unit: 'K' },
]
</script>