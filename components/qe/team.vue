<template>
  <div class="py-24 sm:py-32" v-motion-pop-visible>
    <div class="relative isolate">
      <div class="mx-auto max-w-7xl sm:px-6 lg:px-8">
        <div class="flex flex-col mx-auto bg-white/5 max-w-2xl py-16 px-6 ring-1 ring-white/10 gap-16 sm:rounded-3xl sm:p-8 lg:flex-row lg:max-w-none lg:mx-0 lg:py-20 lg:items-center xl:px-20 xl:gap-x-20">
          <div class="flex-auto w-full">
            <h2 class="font-bold text-white tracking-tight text-3xl sm:text-4xl">Join $IXO DAO</h2>
            <p class="mt-6 text-lg text-gray-300 leading-8">We’re a dynamic group of individuals who are passionate about what we do and dedicated to expanding Quantum Entanglement to more Web3 citizens.</p>
            <ul role="list" class="mt-10 text-base text-white grid leading-7 gap-x-8 gap-y-3 grid-cols-1 sm:grid-cols-2">
              <template v-for="(benefit, index) in benefits" :key="benefit">
                <li class="flex gap-x-3" v-motion-slide-visible-right v-if="index % 2">
                  <CheckCircleIcon class="flex-none h-7 w-5" aria-hidden="true" />
                  {{ benefit }}
                </li>
                <li class="flex gap-x-3" v-motion-slide-visible-left v-else>
                  <CheckCircleIcon class="flex-none h-7 w-5" aria-hidden="true" />
                  {{ benefit }}
                </li>
              </template>
            </ul>
            <div class="flex mt-10 justify-end">
              <NuxtLink to="/ixo/dao" class="font-semibold text-sm text-lime-400 leading-6">Learn more <span aria-hidden="true">&rarr;</span></NuxtLink>
            </div>
          </div>
        </div>
      </div>
      <div class="flex transform-gpu inset-x-0 -top-16 -z-10 absolute justify-center overflow-hidden blur-3xl" aria-hidden="true">
        <div class="bg-gradient-to-r flex-none from-[#80caff] to-[#4f46e5] opacity-25 w-[82.375rem] aspect-[1318/752]" style="clip-path: polygon(73.6% 51.7%, 91.7% 11.8%, 100% 46.4%, 97.4% 82.2%, 92.5% 84.9%, 75.7% 64%, 55.3% 47.5%, 46.5% 49.4%, 45% 62.9%, 50.3% 87.2%, 21.3% 64.1%, 0.1% 100%, 5.4% 51.1%, 21.4% 63.9%, 58.9% 0.2%, 73.6% 51.7%)" />
      </div>
    </div>
  </div>
</template>

<script setup>
import { CheckCircleIcon } from '@heroicons/vue/20/solid'

const benefits = [
  'Dedicated $QE20 Airdrop',
  'Higher affiliate rate',
  'Monthly top 100 contributors platform profit share',
  'Priority trial rights for new product features',
  'Leadership of Quantum Entanglement in your area',
  'Event support sponsorship',
]
</script>