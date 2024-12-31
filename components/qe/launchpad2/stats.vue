<script setup lang="ts">
const { launchpadStatsMap, loadLaunchpadStats, isLaunchpadStatsLoading } = $(ixoQE721Store());
const { address } = $(rwaAuthStore());

const data = $computed(() => launchpadStatsMap[address] || {});

const stats = $computed(() => {
  const boughtCount = data.ownedNFT + data.ownedFT;
  return [
    { name: "Total Sold", value: numberFormat(formatEther((data.totalSold || 0) + "")), unit: "$QE" },
    { name: "All Launched", value: data.allLaunchCount || 0, unit: "Projects" },
    { name: "You Owned", value: data.projectOwned || 0, unit: "$QE721" },
    { name: "You Bought", value: boughtCount || 0, unit: "$QE1155" },
  ];
});

const isShowBtn = (stat) => {
  return ["You Owned", "You Bought"].includes(stat.name);
};

const btnClick = (stat) => {
  const linkMap = {
    "You Owned": "/ixo/launchpad/owned",
    "You Bought": "/ixo/launchpad/bought",
  };
  navigateTo(linkMap[stat.name]);
};

watchEffect(async () => {
  if (!address) return;
  await loadLaunchpadStats(address);
});
</script>
<template>
  <BsLoading :isLoading="isLaunchpadStatsLoading" class="rounded-xl bg-gray-900 overflow-hidden">
    <div class="mx-auto max-w-7xl">
      <div class="bg-white/5 gap-px grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4">
        <div v-for="stat in stats" :key="stat.name" class="bg-gray-900 py-6 px-4 sm:px-6 lg:px-8">
          <p class="font-medium text-sm text-gray-400 leading-6">{{ stat.name }}</p>
          <div class="flex-bc mt-2">
            <div flex gap-x-2 items-baseline>
              <span class="font-semibold text-white tracking-tight text-4xl">{{ stat.value }}</span>
              <span v-if="stat.unit" class="text-sm text-gray-400">{{ stat.unit }}</span>
            </div>
            <!-- <BsBtnPlain v-if="isShowBtn(stat)" @click="btnClick(stat)" class="text-xs! py-1! px-2!">View</BsBtnPlain> -->
          </div>
        </div>
      </div>
    </div>
  </BsLoading>
</template>
