<script setup lang="ts">
const { name, isLogin } = $(supabaseStore());

onMounted(() => {
  const redirectPath = `${location.origin}${location.pathname}?showInviteDialog=yes`;
  update("redirectPath", redirectPath);
});

const { update, chain, currency, gasBalance, network, updateUserBalance, isUpdatingUserBalance, bstSwapBalance, bstEntropyBalance } = $(
  rwaAuthStore()
);
const { isLoading, doSubmit, codePrice, codeTypeList } = $(inviteCodeStore());
let { codeType } = $(inviteCodeStore());

const { payTokenList, payBy } = $(appStore());
</script>

<template>
  <div class="rounded-xl flex flex-col space-y-5 border-1 text-white text-sm py-8 px-6">
    <div flex-bc>
      <span>Invite code type</span>
      <span>
        <BsFormSelect v-model="codeType" :list="codeTypeList" />
      </span>
    </div>
    <div flex-bc>
      <span>Price</span>
      <span text-rainbow>{{ codePrice }} $QE</span>
    </div>
    <div>
      You will earn <span class="text-rainbow text-lg">{{ codePrice * 2 }} $QE</span> once someone use your invite code to buy the $QE721 NFT.
    </div>
    <div flex-bc>
      <span flex-bc>Pay By</span>
      <BsFormSelect id="payBy" v-model="payBy" :list="payTokenList" class="" />
    </div>
    <div flex-bc>
      <div flex-bc>
        <span class="mr-2">Payment Balance</span>
        <span v-if="payBy === '$QESwap'">[<NuxtLink :to="`/bridge?t=${network}`" target="_blank" class="text-red">Deposit More</NuxtLink>]</span>
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
    <div pt-5>
      <BsBtnPlain @click="doSubmit" :isLoading="isLoading" class="w-full">Buy</BsBtnPlain>
    </div>
  </div>
</template>
