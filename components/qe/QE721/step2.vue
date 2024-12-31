<template>
  <div class="mx-auto max-w-2xl grid gap-x-8 gap-y-16 grid-cols-1 sm:gap-y-20 lg:max-w-none lg:mx-0 lg:grid-cols-2">
    <div flex-cc lg:pr-8 v-motion-slide-left v-motion-slide-visible-left>
      <img src="/img/QE1155.jpg" class="rounded-xl shadow-xl opacity-90 ring-1 ring-white/10" />
    </div>
    <div v-motion-slide-right v-motion-slide-visible-right>
      <div class="mx-8 sm:mx-0 lg:max-w-lg">
        <h2 class="font-semibold text-base text-lime-400 leading-7">Step 2</h2>
        <p class="font-bold mt-2 text-white tracking-tight text-3xl sm:text-4xl">Launch $QE1155 Project </p>
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
  </div>
</template>

<script setup>
import LineMdTwitterX from '~icons/line-md/twitter-x'
import TeenyiconsViewGridOutline from '~icons/teenyicons/view-grid-outline'
import FluentEmojiRocket from '~icons/fluent-emoji/rocket'

const features = [
  {
    name: 'Initial X Offering.',
    description: 'Provide an Anti Sybil Attacks logic for you to target your first 10K+ high value users.',
    icon: LineMdTwitterX,
  },
  {
    name: 'Sell your $QE1155.',
    description:
      `The $QE1155 has the duality of NFT / FT, so you can sell by 1 NFT or by 10K FT of your $QE1155.`,
    icon: FluentEmojiRocket,
  },

  {
    name: 'Grid Profitable.',
    description: 'Each $QE1155 NFT have a grid in your $QE1155 project, which is a traffic / user share system that make profit for owner.',
    icon: TeenyiconsViewGridOutline,
  },
]
</script>