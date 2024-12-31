<script setup lang="ts">
const title = $ref("Owned - Launchpad - IXO");
const desc = $ref(" The first Fair Mint Token for All X Users");

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
    <QeLaunchpad2Heading pageTitle="You owned Project" />

    <QeLaunchpad2OwnedList />
  </div>
</template>
