<script setup lang="ts">
const title = $ref("Home - Quantum Entanglement");
const desc = $ref("Quantum Entanglement");
const { metadata } = $(supabaseStore());

provide("title", $$(title));
provide("desc", $$(desc));

// put the user's ref link, as every new user need a ref Twitter!!!
const shareLink = $computed(() => `${location.origin}${location.pathname}?ref=${metadata?.user_name}`);

useHead({
  title,
});
definePageMeta({
  layout: "ixo",
  description: `Quantum Entanglement.`,
});
</script>
<template>
  <div>
    <QeHero mt-0 sm:mt-20 />
    <QeTech />
    <QeFeatures />
    <QeStatus />
    <QeComponents />
    <!-- <QeTestimonials /> -->
    <!-- <QeTeam /> -->

    <!-- <QeXrc20Faq bg-white md:rounded-2xl mt-50 /> -->
  </div>
</template>
