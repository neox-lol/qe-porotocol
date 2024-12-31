<script setup lang="ts">
const tokenMeta = $(inject("tokenMeta"));
</script>
<template>
  <div class="mx-auto text-center py-10">
    <h1 class="font-bold text-white mb-10 tracking-tight text-4xl">
      {{ tokenMeta.name }}
      $QE1155 FT
      <br />
      <br />
      <span text-rainbow uppercase text-3xl class="animate-pulse">Tweet to Free Mint</span>
      <br />
    </h1>
    <QeLaunchpad2Progress />
    <QeLaunchpad2TweetToMint />
  </div>
</template>
