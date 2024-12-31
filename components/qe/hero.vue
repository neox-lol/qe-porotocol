<script setup lang="ts">
  import { useMotion } from '@vueuse/motion'

  const wordArr = [
    'ERC20 Token',
    'ERC721 NFT',
    'ERC1155 NFT',
    'Launchpad',
    'Marketplace',
  ]
  // A/An 'ERC20 Token', 'ERC721 NFT', 'ERC1155 NFT', 'Launchpad', 'Marketplace' Made with ERC404Pro | #ERC404 #ERC404Pro
  let index = $ref(0)

  const numberPrefix = $computed(() => {
    if (['a', 'e', 'i', 'o', 'u'].includes(wordArr[index][0].toLowerCase())) {
      return 'An'
    }
    return 'A'
  })
  const updateIndex = (_index) => {
    index = _index
  }

  const heroRef = ref()
  const { variant } = useMotion(heroRef, {
    initial: {
      y: -200,
      scale: 0,
      opacity: 0,
    },
    enter: {
      y: 0,
      scale: 2,
      opacity: 1,
      transition: {
        type: 'spring',
        stiffness: 350,
        damping: 20,
        onComplete: () => {
          variant.value = 'levitate'
        },
      },
    },
    visible: {
      y: 0,
      scale: 1,
      opacity: 1,
      transition: {
        type: 'spring',
        stiffness: 350,
        damping: 20,
        onComplete: () => {
          variant.value = 'levitate'
        },
      },
    },
    levitate: {
      y: 15,
      transition: {
        duration: 2000,
        repeat: Infinity,
        ease: 'easeInOut',
        repeatType: 'mirror',
      },
    },
  })

  const popBottom = {
    initial: { opacity: 0, y: 200, scale: 0 },
    enter: { opacity: 1, y: 0, scale: 2 },
    visible: { opacity: 1, y: 0, scale: 1 },
  }
</script>
<template>
  <div
    class="flex flex-col mx-auto text-center main justify-center items-center">
    <h1
      class="font-bold mb-30 tracking-tight sm:mb-50"
      ref="heroRef">
      <span
        text-rainbow
        text-6xl
        sm:text-8xl
        class="animate-pulse"
        >Quantum Entanglement</span
      >
    </h1>
    <div
      @vue:mounted="(node) => useMotion(node.el, popBottom)"
      class="flex flex-col font-bold text-xl px-2 text-gray-300 leading-6 items-center justify-center sm:flex-row sm:text-3xl sm:leading-12">
      <div flex-cc>
        <span>{{ numberPrefix }}</span>
        <span
          text-rainbow
          font-bold
          text-2xl
          sm:text-6xl
          px-5>
          <VueWriter
            :array="wordArr"
            @index="updateIndex" />
        </span>
      </div>
      <div flex-cc>
        <span>made with</span>
        <span
          text-rainbow
          font-bold
          text-2xl
          sm:text-6xl
          px-5
          >QE Protocol</span
        >
      </div>
    </div>
    <NuxtLink
      to="/launchpad"
      v-motion-slide-bottom
      v-motion-slide-visible-top
      @click="isShow = true"
      class="bg-rainbow flex my-20 py-3 w-80 justify-center items-center border-none! font-bold! rounded-2xl! text-xl! hover:(scale-120 animate-pulse)">
      <span
        i-noto-backhand-index-pointing-right
        w-5
        h-5
        mr-2
        flex />
      Launch Your QE Token
    </NuxtLink>
  </div>
</template>
