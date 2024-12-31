<script setup lang="ts">
const { foo } = defineProps<{
  foo: string;
}>();

let { count } = defineModels<{
  count: number;
}>();

count++;

const stats = [
  { name: "Your Code", value: "0", unit: "" },
  { name: "You Invited", value: "0", unit: "Users" },
  { name: "You Earned", value: "0", unit: "$QE" },
];
</script>

<template>
  <div class="rounded-xl bg-gray-900 mt-10 overflow-hidden">
    <div class="mx-auto max-w-7xl">
      <div class="bg-white/5 gap-px grid grid-cols-1 sm:grid-cols-1 lg:grid-cols-3">
        <div v-for="stat in stats" :key="stat.name" class="bg-gray-900 py-6 px-4 sm:px-6 lg:px-8">
          <p class="font-medium text-sm text-gray-400 leading-6">{{ stat.name }}</p>
          <div class="flex-bc mt-2">
            <div flex gap-x-2 items-baseline>
              <span class="font-semibold text-white tracking-tight text-4xl">{{ stat.value }}</span>
              <span v-if="stat.unit" class="text-sm text-gray-400">{{ stat.unit }}</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
