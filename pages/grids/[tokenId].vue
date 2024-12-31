<script setup lang="ts">
const { loadTokenData, tokenMap, loadTokenOnChainData } = $(ixoQE721Store());

const route = useRoute();
const tokenId = $computed(() => route.params.tokenId);
const tokenData = $computed(() => tokenMap[tokenId] || {});
const tokenMeta = $computed(() => tokenData.meta || {});

provide("tokenData", $$(tokenData));
provide("tokenMeta", $$(tokenMeta));

const title = computed(() => {
  if (!tokenMeta.name) {
    return "loading...";
  }
  return `${tokenMeta.name} - IXO`;
});
useHead({ title });

watchEffect(async () => {
  if (!tokenId) return;
  await loadTokenData(tokenId);
  await loadTokenOnChainData(tokenId);
});

definePageMeta({
  layout: "ixo",
});
</script>
<template>
  <div pt-10 main-px>
    <QeLaunchpad2Heading :pageTitle="tokenMeta.name || ''" />

    <QeLaunchpad2TokenInfo />

    <div v-if="true" id="ft" mb-30>
      <QeLaunchpad2FreeMint />
      <QeLaunchpad2UserReward />
    </div>
    <QeLaunchpad2Grid mx-auto />
  </div>
</template>
