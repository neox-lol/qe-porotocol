<script setup lang="ts">
import LineMdTwitterX from '~icons/line-md/twitter-x'
import IonDiamondOutline from '~icons/ion/diamond-outline'
import TablerError404 from '~icons/tabler/error-404'

const primaryFeatures = [
  {
    name: 'Initial X Offering',
    description:
      'A complete set of verification processes based on X users to Anti Sybil Attacks. In the future, we will further introduce AI big data, etc. To further filter out effective value users.',
    href: '#',
    icon: LineMdTwitterX,
  },
  {
    name: 'Targeting your first 10K high value users',
    description:
      'We provide a set of simple and effective airdrop logic that the first 10K high-net-worth users can participate in, allowing your project to win at the starting line.',
    href: '#',
    icon: IonDiamondOutline,
  },
  {
    name: 'QE Protocol',
    description:
      'One contract includes three types of EIP features: ERC20, ERC721, and ERC1155. It also gives the project party a common benefit sharing mechanism for the early 10K users.',
    href: '#',
    icon: TablerError404,
  },
]


const launchBtnRef = ref()
const { variant } = useMotion(launchBtnRef, {
  initial: {
    y: 50,
    scale: 0,
    opacity: 0,
  },
  enter: {
    y: 0,
    scale: 4,
    opacity: 1,
    transition: {
      type: "spring",
      stiffness: 100,
      damping: 5,
      onComplete: () => {
        variant.value = "levitate";
      },
    },
  },
  visible: {
    y: 0,
    scale: 1,
    opacity: 1,
    transition: {
      type: "spring",
      stiffness: 100,
      damping: 5,
      onComplete: () => {
        variant.value = "levitate";
      },
    },
  },
  levitate: {
    y: 15,
    transition: {
      duration: 900,
      repeat: Infinity,
      ease: "easeInOut",
      repeatType: "mirror",
    },
  },
});
</script>
<template>
  <div class="mx-auto mt-16 max-w-7xl px-6 sm:mt-28 lg:px-8">
    <div class="mx-auto text-center max-w-2xl" v-motion-pop-visible>
      <h2 class="font-semibold text-base text-lime-400 leading-7">Everything you need to Launch</h2>
      <p class="font-bold mt-2 text-white tracking-tight text-3xl sm:text-4xl">Your next Billion Worth Project</p>
    </div>
    <div class="mx-auto mt-16 max-w-2xl sm:mt-20 lg:max-w-none lg:mt-24">
      <dl class="max-w-xl grid gap-x-8 gap-y-16 grid-cols-1 lg:max-w-none lg:grid-cols-3">
        <div v-for="(feature, index) in primaryFeatures" :key="feature.name" class="flex flex-col" v-motion-slide-visible-bottom>
          <dt class="font-semibold text-base text-white leading-7">
            <div class="rounded-lg flex bg-lime-500 h-10 mb-6 w-10 items-center justify-center">
              <component :is="feature.icon" class="h-6 text-white w-6" aria-hidden="true" />
            </div>
            {{ feature.name }}
          </dt>
          <dd class="flex flex-auto flex-col mt-1 text-base text-gray-300 leading-7">
            <p class="flex-auto">{{ feature.description }}</p>
            <!-- <p class="mt-6">
              <a :href="feature.href" class="font-semibold text-sm text-lime-400 leading-6">Learn more <span aria-hidden="true">→</span></a>
            </p> -->
          </dd>
        </div>
      </dl>
    </div>
    <div flex-cc>
      <NuxtLink ref="launchBtnRef" to="/launchpad" class="bg-rainbow flex my-20 py-3 w-100 transition-duration-200 justify-center items-center border-none! font-bold! rounded-2xl! text-xl! hover:(scale-120 animate-pulse) ">
        <span i-emojione-v1-rocket w-5 h-5 mr-2 flex />
        Launch your Billion Project now
      </NuxtLink>
    </div>
  </div>
</template>