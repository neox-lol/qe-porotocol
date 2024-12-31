<script setup lang="ts">
const { loadProject, isLoadingProject, projectMap } = $(ixoQE721Store());
const launchedData = $computed(() => projectMap["launched"] || { items: [], count: 0 });

onMounted(loadProject);
</script>
<template>
  <BsLoading :isLoading="isLoadingProject">
    <ul role="list" class="divide-y divide-gray-800">
      <li v-for="item in launchedData.items" :key="item.email">
        <NuxtLink :to="`/grids/${item.tokenId}`" class="flex py-5 px-6 gap-x-6 justify-between hover:(opacity-80 bg-gray-800) ">
          <div class="flex min-w-0 gap-x-4 items-stretch">
            <div text-white flex-cc font-bold text-3xl>#{{ item.tokenId }}</div>
            <div class="rounded-xl flex-none bg-gray-800 h-20 w-20 overflow-hidden">
              <BsBoxImg :src="item.meta.avatar" alt=""  />
            </div>

            <div class="flex-auto min-w-0 items-stretch">
              <p class="font-semibold text-sm text-white leading-6">
                {{ item.meta.name }}
              </p>
              <p class="mt-1 text-xs text-gray-400 leading-5 truncate">{{ item.meta.desc }}</p>
            </div>
          </div>
          <div class="hidden sm:flex sm:flex-col shrink-0 sm:items-end">
            <p class="text-sm text-white leading-6">{{ item.meta.nftPrice / item.meta.ftSwapUnit }} $QE / FT</p>
            <p class="text-sm text-white leading-6">{{ item.meta.nftPrice }} $QE / NFT</p>
          </div>
          <div class="hidden sm:flex sm:flex-col shrink-0 sm:items-end">
            <p class="text-sm text-gray-400 leading-6">Sold / Total</p>
            <p class="text-sm text-white leading-6">{{ numberFormat(item.totalSold || 0) }} / {{ numberFormat(item.meta.nftPrice * 10000) }} $QE</p>
          </div>
          <div class="hidden sm:flex sm:flex-col shrink-0 sm:items-end">
            <p class="text-sm text-gray-400 leading-6">FT Holders</p>
            <p class="text-sm text-white leading-6">
              {{ item.ftHolders || 0 }}
            </p>
          </div>
          <div class="hidden sm:flex sm:flex-col shrink-0 sm:items-end">
            <p class="text-sm text-gray-400 leading-6">NFT Holders</p>
            <p class="text-sm text-white leading-6">
              {{ item.nftHolders || 0 }}
            </p>
          </div>
        </NuxtLink>
      </li>
    </ul>
  </BsLoading>
</template>
