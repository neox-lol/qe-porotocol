<script setup lang="ts">
const { name, isLogin } = $(supabaseStore());

onMounted(() => {
  const redirectPath = `${location.origin}${location.pathname}?showBuyDialog=yes`;
  update("redirectPath", redirectPath);
});

const {
  doLogin,
  update,
  chain,
  toggle,
  currency,
  gasBalance,
  network,
  updateUserBalance,
  isUpdatingUserBalance,
  bstSwapBalance,
  bstEntropyBalance,
} = $(rwaAuthStore());
const { showDialog, buyType, isTradeable, nftPrice, inviteCode, doMint, isLoading } = $(ixoNFTBuyStore());
let { isShow } = $(ixoNFTBuyStore());
const items = $computed(() => {
  return [
    { name: "Public", checked: buyType === "Public" },
    { name: "X.com", checked: buyType === "X.com" },
    { name: "Pump.Fun", checked: buyType === "Pump.Fun" },
  ];
});

const { payTokenList, payBy } = $(appStore());
</script>

<template>
  <div flex justify="center">
    <BsDialogDefault :show="isShow" :no-padding="true" @close="isShow = false">
      <div class="bg-lime-600 max-w-2xl py-10 px-3 shadow-2xl relative isolate overflow-hidden sm:rounded-3xl sm:px-12 xl:py-8">
        <h2 class="font-bold mx-auto text-center text-white text-xl tracking-tight max-w-2xl sm:text-2xl">Mint QE721 NFT</h2>
        <div flex-cc>
          <BsBtnBlack v-if="!isLogin" @click="doLogin('twitter', toggle)" rounded-full my-10>
            <span i-ci-twitter mr-1></span>
            Auth with Twitter
          </BsBtnBlack>
          <div v-else flex flex-col items-center w-full>
            <div class="mt-10 grid gap-4 grid-cols-3">
              <template v-for="item in items" :key="item.name">
                <BsBtnRainbow v-if="item.checked">{{ item.name }} Sale</BsBtnRainbow>
                <BsBtnDefault v-else @click="showDialog(item.name)">{{ item.name }} Sale</BsBtnDefault>
              </template>
            </div>
            <BsLoading :is-loading="isLoading" class="w-full">
              <div class="rounded-xl flex flex-col space-y-3 border-1 mt-10 text-white text-sm py-8 px-6">
                <div flex-bc>
                  <span>NFT Cell</span>
                  <span>10K Grid Cell Inside</span>
                </div>
                <div flex-bc>
                  <span>FT Amount</span>
                  <span>10K * 10K FT Inside</span>
                </div>
                <div flex-bc>
                  <span text-red font-bold>NFT Tradeable</span>
                  <span text-rainbow uppercase mx-2>{{ isTradeable ? "YES" : "NO" }}</span>
                </div>
                <div flex-bc>
                  <span></span>
                  <span flex-bc text-xs text-right v-if="isTradeable">Public Sale NFT can be transfer or <br />trade in most NFT Marketplace</span>
                  <span text-xs text-right v-else
                    >{{ buyType }} NFT is a <span text-rainbow>Sole Bind Token</span> <br />
                    that can not be transfer</span
                  >
                </div>
                <div divide-y>
                  <div>&nbsp;</div>
                  <div>&nbsp;</div>
                </div>
                <div flex-bc>
                  <span>Price</span>
                  <span>{{ nftPrice }} $QE</span>
                </div>
                <div flex-bc>
                  <span flex-bc>Pay By</span>
                  <BsFormSelect id="payBy" v-model="payBy" :list="payTokenList" class="" />
                </div>
                <div flex-bc>
                  <div flex-bc>
                    <span class="mr-2">Payment Balance</span>
                    <span v-if="payBy === '$QESwap'"
                      >[<NuxtLink :to="`/bridge?t=${network}`" target="_blank" class="text-red">Deposit More</NuxtLink>]</span
                    >
                  </div>
                  <span flex-bc space-x-2>
                    <span v-if="payBy === '$QESwap'">{{ humanFormatEther(bstSwapBalance) }} {{ payBy }}</span>
                    <span v-if="payBy === '$QEEntropy'">{{ humanFormatEther(bstEntropyBalance) }} {{ payBy }}</span>
                    <BsLoadingIcon v-if="isUpdatingUserBalance" />
                    <span v-else i-material-symbols-light-directory-sync cursor-pointer w-5 h-5 @click="updateUserBalance">Reload</span>
                  </span>
                </div>
                <div flex-bc>
                  <label for="currentBalance" class="font-medium text-sm text-white leading-6 block">Gas Token Balance:</label>
                  <div flex-cc>
                    <span font-bold mr-2> {{ numberFormat(gasBalance) }} {{ currency }}</span>
                    <BsLoadingIcon v-if="isUpdatingUserBalance" />
                    <span v-else i-material-symbols-light-directory-sync cursor-pointer w-5 h-5 @click="updateUserBalance">Reload</span>
                  </div>
                </div>
                <BsGasFullfillAlert :chain="chain"></BsGasFullfillAlert>
                <div flex-bc v-if="!isTradeable" text-red>
                  <div>Your {{ buyType }} Handle</div>
                  <div>
                    {{ name }}
                  </div>
                </div>
                <div flex-bc v-if="!isTradeable">
                  <div>Your Invite Code</div>
                  <div>
                    <input
                      id="invite-code"
                      v-model="inviteCode"
                      name="invite-code"
                      type="text"
                      autocomplete="invite-code"
                      required="true"
                      class="rounded-md max-w-sm bg-white/5 border-0 shadow-sm ring-inset text-white py-2 px-3.5 ring-1 ring-white/10 sm:text-sm sm:leading-6 focus:ring-inset focus:ring-white focus:ring-2"
                      placeholder="Enter your invite code"
                    />
                  </div>
                </div>
                <div pt-5>
                  <BsBtnPlain @click="doMint" :isLoading="isLoading" class="w-full">Mint</BsBtnPlain>
                </div>
              </div>
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
