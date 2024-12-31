<script setup lang="ts">
import { CheckIcon } from "@heroicons/vue/20/solid";

const tiers = [
  {
    name: "Public",
    price: "1000 $QE",
    priceSuffix: "/ NFT",
    description: "Public for all web3 citizens.",
    features: [
      "Unlimited for every buyer",
      "8000 Total Supply",
      "NFT can be sold on any marketplace",
      "Every NFT includes 10k Grids",
      "10% fee profit for every grid trade",
    ],
    mostPopular: false,
  },
  {
    name: "X.com",
    price: "300 $QE",
    priceSuffix: "/ NFT",
    description: "Only for X.com users",
    features: [
      "Limited Mint for 1 NFT / X user",
      "1000 Total Supply",
      "NFT can not be sold",
      "Every NFT includes 10k Grids",
      "10% fee profit for every grid trade",
    ],
    mostPopular: true,
  },
  {
    name: "Pump.Fun",
    price: "100 $QE",
    priceSuffix: "/ NFT",
    description: "Only for Pump.Fun users.",
    features: [
      "Limited Mint for 1 NFT / FT user",
      "1000 Total Supply",
      "NFT can not be sold",
      "Every NFT includes 10k Grids",
      "10% fee profit for every grid trade",
    ],
    mostPopular: false,
  },
];

const isHighlight = (feature) => {
  return ["Unknown gift", "Unknown benifit"].includes(feature);
};

const { showDialog } = $(ixoNFTBuyStore());
</script>
<template>
  <div class="mx-auto px-3 lg:(px-4)">
    <div class="mx-auto text-center max-w-4xl">
      <p class="font-bold mt-2 text-white tracking-tight pb-10 text-4xl sm:text-5xl"><span text-rainbow>Limited sale for each round</span></p>
    </div>

    <div v-motion-pop-visible>
      <div class="flex mb-1 justify-between">
        <span class="font-medium text-xl text-rainbow dark:text-white">Round 1</span>
        <span class="font-medium text-xl text-rainbow dark:text-white">45 / 100</span>
      </div>
      <div class="rounded-full bg-gray-200 h-2.5 mt-5 w-full dark:bg-gray-700">
        <div class="bg-rainbow rounded-full h-2.5" style="width: 45%"></div>
      </div>
    </div>

    <div class="mx-auto max-w-md mt-16 grid gap-8 grid-cols-1 isolate lg:max-w-none lg:mx-0 lg:grid-cols-3">
      <template v-for="(tier, index) in tiers" :key="tier.name">
        <div
          v-if="index == 0"
          v-motion-slide-visible-left
          class="transform-gpu transition-all ease-linear hover:(scale-110 ring-lime-500 bg-white/5 ring-2 animate-pulse) "
          :class="[tier.mostPopular ? 'bg-white/5 ring-2 ring-lime-500' : 'ring-1 ring-white/10', 'rounded-3xl p-8 xl:p-10']"
        >
          <div class="flex gap-x-4 items-center justify-between">
            <h3 class="font-semibold text-lg text-white leading-8">{{ tier.name }} Sale</h3>
            <p v-if="tier.mostPopular" class="rounded-full font-semibold bg-lime-500 text-xs text-white py-1 px-2.5 leading-5">Recommented</p>
          </div>
          <p class="mt-4 text-sm text-gray-300 leading-6">{{ tier.description }}</p>
          <p class="flex mt-6 gap-x-1 items-baseline">
            <span class="font-bold text-white tracking-tight text-4xl">{{ tier.price }}</span>
            <span class="font-semibold text-sm text-gray-300 leading-6"> {{ tier.priceSuffix }}</span>
          </p>
          <button
            @click="showDialog(tier.name)"
            :aria-describedby="tier.name"
            :class="[
              tier.mostPopular
                ? 'bg-lime-500 text-white shadow-sm hover:bg-lime-400 focus-visible:outline-lime-500'
                : 'bg-white/10 text-white hover:bg-white/20 focus-visible:outline-white',
              'mt-6 block rounded-md py-2 px-3 text-center text-sm font-semibold leading-6 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2',
              'w-full',
            ]"
          >
            Mint
          </button>
          <ul role="list" class="space-y-3 mt-8 text-sm text-gray-300 leading-6 xl:mt-10">
            <li v-for="feature in tier.features" :key="feature" class="flex gap-x-3">
              <CheckIcon class="flex-none h-6 text-white w-5" aria-hidden="true" />
              <span :class="isHighlight(feature) ? 'text-rainbow' : ''">{{ feature }}</span>
            </li>
          </ul>
        </div>
        <div
          v-if="index == 1"
          v-motion-slide-visible-bottom
          class="transform-gpu transition-all ease-linear hover:(scale-110 ring-lime-500 bg-white/5 ring-2 animate-pulse) "
          :class="[tier.mostPopular ? 'bg-white/5 ring-2 ring-lime-500' : 'ring-1 ring-white/10', 'rounded-3xl p-8 xl:p-10']"
        >
          <div class="flex gap-x-4 items-center justify-between">
            <h3 :id="tier.name" class="font-semibold text-lg text-white leading-8">{{ tier.name }} Sale</h3>
            <p v-if="tier.mostPopular" class="rounded-full font-semibold bg-lime-500 text-xs text-white py-1 px-2.5 leading-5">Recommented</p>
          </div>
          <p class="mt-4 text-sm text-gray-300 leading-6">{{ tier.description }}</p>
          <p class="flex mt-6 gap-x-1 items-baseline">
            <span class="font-bold text-white tracking-tight text-4xl">{{ tier.price }}</span>
            <span class="font-semibold text-sm text-gray-300 leading-6"> {{ tier.priceSuffix }}</span>
          </p>
          <button
            @click="showDialog(tier.name)"
            :aria-describedby="tier.name"
            :class="[
              tier.mostPopular
                ? 'bg-lime-500 text-white shadow-sm hover:bg-lime-400 focus-visible:outline-lime-500'
                : 'bg-white/10 text-white hover:bg-white/20 focus-visible:outline-white',
              'mt-6 block rounded-md py-2 px-3 text-center text-sm font-semibold leading-6 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 w-full',
            ]"
          >
            Mint
          </button>
          <ul role="list" class="space-y-3 mt-8 text-sm text-gray-300 leading-6 xl:mt-10">
            <li v-for="feature in tier.features" :key="feature" class="flex gap-x-3">
              <CheckIcon class="flex-none h-6 text-white w-5" aria-hidden="true" />
              <span :class="isHighlight(feature) ? 'text-rainbow' : ''">{{ feature }}</span>
            </li>
          </ul>
        </div>
        <div
          v-if="index == 2"
          v-motion-slide-visible-right
          class="transform-gpu transition-all ease-linear hover:(scale-110 ring-lime-500 bg-white/5 ring-2 animate-pulse) "
          :class="[tier.mostPopular ? 'bg-white/5 ring-2 ring-lime-500' : 'ring-1 ring-white/10', 'rounded-3xl p-8 xl:p-10']"
        >
          <div class="flex gap-x-4 items-center justify-between">
            <h3 :id="tier.name" class="font-semibold text-lg text-white leading-8">{{ tier.name }} Sale</h3>
            <p v-if="tier.mostPopular" class="rounded-full font-semibold bg-lime-500 text-xs text-white py-1 px-2.5 leading-5">Recommented</p>
          </div>
          <p class="mt-4 text-sm text-gray-300 leading-6">{{ tier.description }}</p>
          <p class="flex mt-6 gap-x-1 items-baseline">
            <span class="font-bold text-white tracking-tight text-4xl">{{ tier.price }}</span>
            <span class="font-semibold text-sm text-gray-300 leading-6"> {{ tier.priceSuffix }}</span>
          </p>
          <button
            @click="showDialog(tier.name)"
            :aria-describedby="tier.name"
            :class="[
              tier.mostPopular
                ? 'bg-lime-500 text-white shadow-sm hover:bg-lime-400 focus-visible:outline-lime-500'
                : 'bg-white/10 text-white hover:bg-white/20 focus-visible:outline-white',
              'mt-6 block rounded-md py-2 px-3 text-center text-sm font-semibold leading-6 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 w-full',
            ]"
          >
            Mint
          </button>
          <ul role="list" class="space-y-3 mt-8 text-sm text-gray-300 leading-6 xl:mt-10">
            <li v-for="feature in tier.features" :key="feature" class="flex gap-x-3">
              <CheckIcon class="flex-none h-6 text-white w-5" aria-hidden="true" />
              <span :class="isHighlight(feature) ? 'text-rainbow' : ''">{{ feature }}</span>
            </li>
          </ul>
        </div>
      </template>
    </div>
    <QeQE721BuyDialog />
    <QeQE721InviteDialog />
  </div>
</template>
