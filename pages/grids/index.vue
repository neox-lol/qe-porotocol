<script setup lang="ts">
const title = $ref("Launchpad - IXO");

useHead({
  title,
});
definePageMeta({
  layout: "ixo",
  description: `Quantum Entanglement Token.`,
});
</script>
<template>
  <div pt-10 main-px>
    <QeLaunchpad2Stats mb-10 />
    <QeLaunchpad2List />
  </div>
</template>
