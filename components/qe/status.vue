<template>
  <div class="mx-auto mt-28 max-w-7xl px-6 sm:mt-56 lg:px-8">
    <div class="mx-auto max-w-2xl lg:max-w-xl lg:mx-0" v-motion-slide-visible-right>
      <h2 class="font-semibold text-base text-lime-400 leading-8">Our track record</h2>
      <p class="font-bold mt-2 text-white tracking-tight text-3xl sm:text-4xl">Trusted by thousands of Web3 citizen &nbsp;worldwide</p>
      <!-- <p class="mt-6 text-lg text-gray-300 leading-8">Since we launch, we gain a wonderfull record till now.</p> -->
    </div>
    <dl class=" mx-auto mt-16 text-white text-right grid gap-x-8 gap-y-10 grid-cols-1 sm:mt-20 sm:gap-y-16 sm:grid-cols-2 lg:max-w-none lg:mx-0 lg:grid-cols-3">
      <div v-motion-slide-visible-bottom v-for="stat in stats" :key="stat.id" class="border-l flex flex-col border-white/10 pl-6 text-4xl gap-y-3" v-element-visibility="inView(stat)">
        <dt class="text-sm leading-6">{{ stat.name }}</dt>
        <dd class="order-first font-semibold tracking-tight ">
          <vue3-autocounter :ref="el => stat.theRef.value = el" :startAmount="0" :endAmount="stat.value" :duration="1" prefix="" suffix="" separator="" decimalSeparator="" :decimals="0" :autoinit="false" />
          {{ stat.unit }}
        </dd>
      </div>
    </dl>
  </div>
</template>

<script setup lang="ts">
import Vue3Autocounter from 'vue3-autocounter';
import { vElementVisibility } from '@vueuse/components'

const inView = item => {
  return isShow => {
    if (!isShow) return
    item.theRef?.value?.start()
  }
}

const stats = $computed(() => {
  return [
    { theRef: ref(null), id: 1, name: '$QE20 Minted', value: 8927, unit: 'M' },
    { theRef: ref(null), id: 2, name: '$QE721 NFT Project Issued', value: 2394, unit: '/ 10000' },
    { theRef: ref(null), id: 3, name: '$QE1155 Token Sold', value: 2846, unit: 'M / 1000 B' },
  ]
})

</script>