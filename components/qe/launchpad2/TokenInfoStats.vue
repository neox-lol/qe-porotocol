<script setup lang="ts">
const tokenData = $(inject("tokenData"));

const { tokenOnChainDataMap, isOnChainDataLoading } = $(ixoQE721Store());

const tokenOnChainData = $computed(() => tokenOnChainDataMap[tokenData.tokenId] || {});

const stats = $computed(() => {
  return [
    { name: "Total Sold", value: formatEther((tokenOnChainData.totalSold || 0) + ""), unit: "$QE" },
    { name: "Holders", value: tokenOnChainData.ftHolders + tokenOnChainData.nftHolders || 0, unit: "" },
    { name: "$QE1155 NFT", value: tokenOnChainData.nftCount || 0 },
    { name: "$QE1155 FT", value: tokenOnChainData.ftCount || 0 },
  ];
});
</script>
<template>
  <BsLoading class="" :isLoading="isOnChainDataLoading" text="Loading token on chain data...">
    <div class="mx-auto w-full max-w-7xl">
      <div class="bg-white/5 rounded-2xl gap-px grid grid-cols-1 overflow-hidden sm:grid-cols-2 lg:grid-cols-4">
        <div v-for="stat in stats" :key="stat.name" class="bg-gray-900 py-6 px-4 sm:px-6 lg:px-8">
          <p class="font-medium text-sm text-gray-400 leading-6">{{ stat.name }}</p>
          <p class="flex mt-2 gap-x-2 items-baseline">
            <span class="font-semibold text-white tracking-tight text-4xl">{{ stat.value }}</span>
            <span v-if="stat.unit" class="text-sm text-gray-400">{{ stat.unit }}</span>
          </p>
        </div>
      </div>
    </div>
  </BsLoading>
</template>
