<script setup lang="ts">
import { useClipboard } from '@vueuse/core'

const requiredMiniAmount = 4
const waitForCollectAmount = 1

const percent = $computed(() => waitForCollectAmount > requiredMiniAmount ? requiredMiniAmount : waitForCollectAmount)
const r = 80
const circumference = 2 * 22 / 7 * r
const offset = $computed(() => circumference - percent / requiredMiniAmount * circumference)
const activityItems = [
  {
    user: {
      name: 'Michael Foster',
      imageUrl:
        'https://images.unsplash.com/photo-1519244703995-f4e0f30006d5?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80',
    },
    projectName: 'ios-app',
    commit: '2d89f0c8',
    branch: 'main',
    date: '1h',
    dateTime: '2023-01-23T11:00',
  },
  {
    user: {
      name: 'Lindsay Walton',
      imageUrl:
        'https://images.unsplash.com/photo-1517841905240-472988babdf9?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80',
    },
    projectName: 'mobile-api',
    commit: '249df660',
    branch: 'main',
    date: '3h',
    dateTime: '2023-01-23T09:00',
  },
  {
    user: {
      name: 'Courtney Henry',
      imageUrl:
        'https://images.unsplash.com/photo-1438761681033-6461ffad8d80?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80',
    },
    projectName: 'ios-app',
    commit: '11464223',
    branch: 'main',
    date: '12h',
    dateTime: '2023-01-23T00:00',
  },
  {
    user: {
      name: 'Courtney Henry',
      imageUrl:
        'https://images.unsplash.com/photo-1438761681033-6461ffad8d80?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80',
    },
    projectName: 'tailwindui.com',
    commit: 'dad28e95',
    branch: 'main',
    date: '2d',
    dateTime: '2023-01-21T13:00',
  },
]

const { alertSuccess } = $(notificationStore())

const { shareLink } = $(supabaseStore())

const source = $computed(() => shareLink)
const { copy } = useClipboard({ source })

const doCopy = () => {
  copy(source)
  alertSuccess('Copy succeed!')
}
</script>

<template>
  <div rounded-xl bg-gray-900 p-5 sm:p-10>
    <h2 text-white text-2xl text-center py-5 mb-5>Invite new user to get <span text-rainbow>$QE20 airdrop</span></h2>
    <div flex-row space-y-10 class="sm:(flex-bc space-x-10 space-y-0) ">
      <div flex-1 border-1 rounded-xl border-gray-700 h-full flex items-center justify-center flex-col>
        <div class="flex items-center justify-center">
          <svg class="h-72 transform w-72 -rotate-90">
            <circle cx="145" cy="145" :r="r" stroke="currentColor" stroke-width="15" fill="transparent" class="text-gray-700" />
            <circle cx="145" cy="145" :r="r" stroke="currentColor" stroke-width="15" fill="transparent" :stroke-dasharray="circumference" :stroke-dashoffset="offset" class="text-indigo-500 " />
          </svg>
          <span class="text-white text-3xl absolute">{{ waitForCollectAmount }} / {{ requiredMiniAmount }}</span>
        </div>
        <BsBtnIndigo rounded-xl @click="doCollect" :disabled="waitForCollectAmount < requiredMiniAmount" :isLoading="isLoading">
          Collect 10K $QE
        </BsBtnIndigo>
        <div text-gray-5 my-10 px-5 text-center>
          Once you invite {{ requiredMiniAmount }} new users, you can collect 10K $QE
        </div>
      </div>
      <div flex-1 h-full>
        <div space-y-4>
          <label for="invite-link" class="font-medium text-lg text-white leading-6 block">Your invite link</label>
          <div class="flex pb-5 items-center">
            <input id="invite-link" type="url" class="rounded-md bg-white/5 border-0 flex-1 shadow-sm ring-inset text-white py-2 px-3.5 ring-0 ring-white/10 select-all sm:text-sm sm:leading-6 focus:ring-inset focus:ring-white focus:ring-2 " disabled :value="shareLink" />
            <BsBtnIndigo @click="doCopy" class="ml-2 py-3!">
              <span i-bxs-copy ml-1></span>
            </BsBtnIndigo>
          </div>
        </div>
        <ul role="list" class="divide-y  divide-white/5 w-full">
          <li v-for="item in activityItems" :key="item.commit" class="py-4">
            <div class="flex gap-x-3 items-center">
              <img :src="item.user.imageUrl" alt="" class="rounded-full flex-none bg-gray-800 h-10 w-10" />
              <div flex-1>
                <h3 class="flex-auto font-semibold text-sm text-white leading-6 truncate">{{ item.user.name }}</h3>
                <p class="text-sm text-gray-500 truncate">
                  <time :datetime="item.dateTime" class="flex-none text-xs text-gray-500">Invited {{ item.date }} ago</time>
                </p>
              </div>
              <div text-sm text-gray-400 text-right>
                2.5K $QE
                <br /> Earned
              </div>
            </div>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>