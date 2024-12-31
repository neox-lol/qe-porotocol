<script setup lang="ts">
import LineMdTwitterX from '~icons/line-md/twitter-x'
import SimpleIconsBitcoin from '~icons/simple-icons/bitcoin'
import TablerError404 from '~icons/tabler/error-404'
import FluentArrowTrendingLines20Filled from '~icons/fluent/arrow-trending-lines-20-filled'
import TeenyiconsViewGridOutline from '~icons/teenyicons/view-grid-outline'

import {
  RocketLaunchIcon,
} from '@heroicons/vue/20/solid'


const values = [
  {
    name: '$QE',
    description: `The first Smart Inscription on X Chain. It's the functional token for Quantum Entanglement. Required in various situations. No investment value!`,
    icon: LineMdTwitterX,
  },
  {
    name: '$QE721',
    description: '10K Total Supply, The owner of the $QE721 got a lot of benefit for long run, eg: IQEO Sell Income, platform Trading fee sharing.',
    icon: TablerError404,
  },
  {
    name: '$QE1155',
    description: `$QE721 can start IQEO via sold $QE1155 which has the duality of NFT and FT. User can swap 10K FT to get 1 NFT, or swap 1 NFT to get 10K FT.`,
    icon: SimpleIconsBitcoin,
  },
  {
    name: 'Launchpad',
    description: `$QE1155 new project launch here, It's the feed stream for IQEO events, providing a platform for users to discover high-quality $QE721 projects.`,
    icon: RocketLaunchIcon,
  },
  {
    name: 'Marketplace',
    description: 'The Quantum Entanglement builtin DEX, staking, and Pool modules provide an efficient, robust, and elegant decentralized market for $QE20, $QE721, and $QE1155.',
    icon: FluentArrowTrendingLines20Filled,
  },
  {
    name: 'Grid',
    description: 'All 10K $QE721 NFT list on the grid that provides a visual map for our users, it can provide a farm function to generate profit from traffic.',
    icon: TeenyiconsViewGridOutline,
  },
]
</script>
<template>
  <div class="mx-auto mt-32 max-w-7xl px-6 sm:mt-40 lg:px-8">
    <div class="flex flex-col text-right justify-center items-end" v-motion-slide-visible-left>
      <h2 class="font-semibold text-base text-lime-400 leading-8">Core Componets</h2>
      <p class="font-bold mt-2 text-white tracking-tight max-w-2xl text-3xl sm:text-4xl lg:max-w-xl lg:mx-0">
        The <span text-rainbow>Quantum Entanglement</span> components
      </p>
      <!-- <p class="mt-6 text-lg text-gray-300 leading-8">Since we launch, we gain a wonderfull record till now.</p> -->
    </div>
    <dl class="mx-auto mt-16 text-base max-w-2xl grid text-gray-300 leading-7 gap-8 grid-cols-1 sm:grid-cols-2 lg:max-w-none lg:mx-0 lg:gap-x-16">
      <template v-for="(value, index) in values" :key="value.name">
        <div class="pl-9 relative" v-motion-slide-visible-right v-if="index % 2">
          <dt class="font-semibold text-white inline">
            <component :is="value.icon" class="h-5 top-1 left-1 text-lime-500 w-5 absolute" aria-hidden="true" />
            <span text-rainbow>{{ value.name }}</span>
          </dt>
          {{ ' ' }}
          <dd class="inline">{{ value.description }}</dd>
        </div>
        <div class="pl-9 relative" v-motion-slide-visible-left v-else>
          <dt class="font-semibold text-white inline">
            <component :is="value.icon" class="h-5 top-1 left-1 text-lime-500 w-5 absolute" aria-hidden="true" />
            <span text-rainbow>{{ value.name }}</span>
          </dt>
          {{ ' ' }}
          <dd class="inline">{{ value.description }}</dd>
        </div>
      </template>
    </dl>
  </div>
</template>