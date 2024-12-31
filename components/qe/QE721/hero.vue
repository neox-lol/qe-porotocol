<script setup lang="ts">
const { isShow } = $(inviteCodeStore());
</script>
<template>
  <div class="mx-auto text-center py-20">
    <h1 class="font-bold my-10 text-white tracking-tight text-4xl sm:text-6xl">
      $QE721 NFT
      <br />
      <br />
      <span text-rainbow uppercase text-6xl sm:text-8xl class="animate-pulse">10K Limited</span>
      <br />
    </h1>
    <p class="text-xl px-2 text-gray-300 leading-8">
      The ownership of your <span text-rainbow> QE Token </span> Launch, bring the <span text-rainbow> duality of NFT / FT </span> to your holders
      without any code.
    </p>
    <div flex-cc space-x-10>
      <NuxtLink
        to="#price"
        v-motion-slide-bottom
        v-motion-slide-visible-top
        class="bg-rainbow flex my-20 py-3 w-80 justify-center items-center border-none! font-bold! rounded-2xl! text-xl! hover:(scale-120 animate-pulse) "
      >
        <span i-noto-backhand-index-pointing-down w-5 h-5 mr-2 flex />
        Mint Now!
      </NuxtLink>
      <NuxtLink
        v-motion-slide-bottom
        v-motion-slide-visible-top
        @click="isShow = true"
        class="bg-rainbow cursor-pointer flex my-20 py-3 w-80 justify-center items-center border-none! font-bold! rounded-2xl! text-xl! hover:(scale-120 animate-pulse) "
      >
        <span i-mdi-share-variant w-5 h-5 mr-2 flex />
        Invite to Earn
      </NuxtLink>
    </div>
  </div>
</template>
