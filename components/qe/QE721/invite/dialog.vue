<script setup lang="ts">
const { isLogin } = $(supabaseStore());

onMounted(() => {
  const redirectPath = `${location.origin}${location.pathname}?showInviteDialog=yes`;
  update("redirectPath", redirectPath);
});

const { doLogin, update, toggle } = $(rwaAuthStore());
let { isShow, currentTab, tabs, isLoading } = $(inviteCodeStore());
</script>

<template>
  <div flex justify="center">
    <BsDialogDefault :show="isShow" :no-padding="true" @close="isShow = false">
      <div class="bg-lime-600 max-w-2xl py-8 px-3 shadow-2xl relative isolate overflow-hidden sm:rounded-3xl sm:px-8 xl:py-10">
        <h2 class="font-bold mx-auto text-center text-white text-xl mb-5 tracking-tight max-w-2xl sm:text-2xl">Invite to Earn</h2>
        <div flex-cc md:w-xl>
          <BsBtnBlack v-if="!isLogin" @click="doLogin('twitter', toggle)" rounded-full my-10>
            <span i-ci-twitter mr-1></span>
            Auth with Twitter
          </BsBtnBlack>
          <div v-else flex flex-col items-center w-full>
            <BsLoading :is-loading="isLoading" class="w-full">
              <div class="border-b border-gray-200 mb-10">
                <nav class="flex -mb-px space-x-2" aria-label="Tabs">
                  <button
                    v-for="tab in tabs"
                    :key="tab.name"
                    @click="currentTab = tab.name"
                    :class="[
                      tab.current ? 'border-white text-white' : 'border-transparent text-gray-400 hover:border-white hover:text-white ',
                      'w-1/4 border-b-2 py-4 px-1 text-center text-sm font-medium',
                    ]"
                    :aria-current="tab.current ? 'page' : undefined"
                  >
                    {{ tab.name }}
                  </button>
                </nav>
              </div>

              <QeQE721InviteRank v-if="currentTab === 'Rank'" />
              <QeQE721InviteCodeList v-if="currentTab === 'Your Code'" />
              <QeQE721InviteForm v-if="currentTab === 'Buy Code'" />
            </BsLoading>
          </div>
        </div>
        <svg viewBox="0 0 1024 1024" class="h-[64rem] top-1/2 left-1/2 w-[64rem] -z-10 -translate-x-1/2 absolute" aria-hidden="true">
          <circle cx="512" cy="512" r="512" fill="url(#759c1415-0410-454c-8f7c-9a820de03641)" fill-opacity="0.7" />
          <defs>
            <radialGradient
              id="759c1415-0410-454c-8f7c-9a820de03641"
              cx="0"
              cy="0"
              r="1"
              gradientUnits="userSpaceOnUse"
              gradientTransform="translate(512 512) rotate(90) scale(512)"
            >
              <stop stop-color="#7775D6" />
              <stop offset="1" stop-color="#E935C1" stop-opacity="0" />
            </radialGradient>
          </defs>
        </svg>
      </div>
    </BsDialogDefault>
  </div>
</template>
