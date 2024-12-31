<template>
  <div class="mx-auto max-w-2xl grid gap-x-8 gap-y-16 grid-cols-1 sm:gap-y-20 lg:max-w-none lg:mx-0 lg:grid-cols-2">
    <div flex-cc sm:hidden v-motion-slide-right v-motion-slide-visible-right>
      <img src="/img/QE721.jpg" class="rounded-xl shadow-xl mx-8 opacity-80 ring-1 ring-white/10 sm:mx-0" />
    </div>
    <div v-motion-slide-left v-motion-slide-visible-left class="px-8 lg:pr-8">
      <div class="lg:max-w-lg">
        <h2 class="font-semibold text-base text-lime-400 leading-7">Step 1</h2>
        <p class="font-bold mt-2 text-white tracking-tight text-3xl sm:text-4xl">Mint a $QE721 NFT</p>
        <dl class="max-w-xl space-y-8 mt-10 text-base text-gray-300 leading-7 lg:max-w-none">
          <div v-for="feature in features" :key="feature.name" class="pl-9 relative">
            <dt class="font-semibold text-white inline">
              <component :is="feature.icon" class="h-5 top-1 left-1 text-lime-500 w-5 absolute" aria-hidden="true" />
              {{ feature.name }}
            </dt>
            {{ ' ' }}
            <dd class="inline">{{ feature.description }}</dd>
          </div>
        </dl>
      </div>
    </div>
    <div hidden class="sm:(flex-cc flex) " v-motion-slide-right v-motion-slide-visible-right>
      <img src="/img/QE721.jpg" class="rounded-xl shadow-xl mx-8 opacity-80 ring-1 ring-white/10 sm:mx-0" />
    </div>
  </div>
</template>

<script setup>
import IconParkSolidStockMarket from '~icons/icon-park-solid/stock-market'
import TablerError404 from '~icons/tabler/error-404'
import TeenyiconsViewGridOutline from '~icons/teenyicons/view-grid-outline'

const features = [
  {
    name: 'Tradable.',
    description:
      `It works like a ERC721 NFT, so it can be trade on any NFT marketplace(X.com Sale and Pump.Fun Sale is SBT, so it can not be trade).`,
    icon: IconParkSolidStockMarket,
  },
  {
    name: 'ERC404Pro.',
    description: 'One $QE721 can create a new $QE1155 project, which has the duality of NFT / FT aka ERC404Pro.',
    icon: TablerError404,
  },
  {
    name: 'Grid Profitable.',
    description: 'Each $QE721 have a grid on our Grid platform, which is a traffic / user share system that make profit for owner.',
    icon: TeenyiconsViewGridOutline,
  },
]
</script>