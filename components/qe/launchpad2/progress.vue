<script setup lang="ts">
const tokenMeta = $(inject("tokenMeta"));
const { isLoading } = $(ixoQE721Store());

const minted = $computed(() => (tokenMeta.freeMintedUserCount || 0) * tokenMeta.freeMintAmountPerUser);

const freeMintSupply = $computed(() => tokenMeta.freeMintUserAmount * tokenMeta.freeMintAmountPerUser);
const percentage = $computed(() => (minted / freeMintSupply).toFixed(4) * 100);
</script>
<template>
  <BsLoading :isLoading="isLoading" px-10 sm:px-6 lg:px-8>
    <div flex-bc text-gray-2 text-sm mb-2>
      <span>Minted: {{ numberFormat(minted) }}</span>
      <span> {{ percentage }}%</span>
      <span>Free mint total supply: {{ numberFormat(freeMintSupply) }}</span>
    </div>
    <progress
      v-if="freeMintSupply"
      aria-labelledby="progress-label"
      id="progress"
      :max="freeMintSupply"
      :value="minted"
      class="rounded w-full overflow-hidden"
    ></progress>
  </BsLoading>
</template>
