<script setup lang="ts">
const title = $ref("ERC404Pro - Quantum Entanglement");
const desc = $ref("ERC404Pro - Quantum Entanglement");

provide("title", $$(title));
provide("desc", $$(desc));

useHead({
  title,
});
definePageMeta({
  layout: "ixo",
  description: `Quantum Entanglement Token.`,
});
</script>
<template>
  <div>
    <QeQE721Hero v-motion-pop v-motion-pop-visible />
    <QeQE721Step1 v-motion-slide-bottom v-motion-slide-visible-top />
    <div id="price"></div>
    <QeQE721Price v-motion-slide-visible-bottom v-motion-slide-bottom pt-40 />
    <QeQE721Step2 v-motion-slide-bottom v-motion-slide-visible-top mt-40 />
    <div flex-cc>
      <NuxtLink
        to="/grids/create"
        v-motion-slide-bottom
        v-motion-slide-visible-top
        @click="isShow = true"
        class="bg-rainbow flex my-20 py-3 w-80 justify-center items-center border-none! font-bold! rounded-2xl! text-xl! hover:(scale-120 animate-pulse)"
      >
        <span i-noto-backhand-index-pointing-right w-5 h-5 mr-2 flex />
        Launch Now
      </NuxtLink>
    </div>
    <QeQE721Faq bg-white md:rounded-2xl mt-20 v-motion-slide-visible-bottom />
  </div>
</template>
