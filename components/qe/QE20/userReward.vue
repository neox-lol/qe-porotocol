<script setup lang="ts">
const { loadRewardItems, isLoading, count, items } = $(ixoStore());
const { linkToExplorer, writeContract } = $(rwaAuthStore());
onMounted(async () => {
  await loadRewardItems("xrc20");
});

const isDebug = $(inject("isDebug"));

let isSending = $ref(false);
const sendAIEntropy = async (item, amount) => {
  if (isSending) return;
  isSending = true;
  try {
    amount = parseEther("" + amount);
    await writeContract("AIEntropy", "transfer", {}, item.to, amount);
  } catch (err) {
    console.log(`====> err :`, err);
  }
  isSending = false;
};
</script>

<template>
  <div>
    <h2 class="flex font-semibold text-base text-white leading-7 items-center main-px">
      <div class="border-b flex border-white/40 pb-3">
        <span mr-4 text-lg>Total Mint $QE:</span>
        <BsLoadingIcon v-if="isLoading" />
        <span v-else> {{ numberFormat(count * 1000) }} </span>
      </div>
    </h2>
    <BsLoading class="py-5" :is-loading="isLoading">
      <table class="mt-6 text-left w-full whitespace-nowrap">
        <!-- <colgroup>
          <col class="w-full sm:w-4/12" />
          <col class="lg:w-4/12" />
          <col class="lg:w-2/12" />
        </colgroup> -->
        <thead class="border-b border-white/10 text-sm text-white leading-6">
          <tr>
            <th scope="col" class="font-semibold py-2 pr-8 pl-4 sm:pl-6 lg:pl-8">User</th>
            <th scope="col" class="font-semibold py-2 pr-8 pl-0">Reward</th>
            <th scope="col" class="font-semibold text-right py-2 pr-4 pl-0 sm:text-left sm:pr-8 lg:pr-20">Status</th>
            <!-- <th scope="col" class="font-semibold py-2 pr-8 pl-0 hidden md:table-cell lg:pr-20">Duration</th> -->
            <th scope="col" class="font-semibold text-right py-2 pr-4 pl-0 sm:pr-6 lg:pr-8">Created at</th>
          </tr>
        </thead>
        <tbody class="divide-y divide-white/5">
          <tr v-for="item in items" :key="item.id">
            <td class="py-4 pr-8 pl-4 sm:pl-6 lg:pl-8">
              <a :href="item?.meta?.link" target="_blank" class="flex gap-x-4 items-center">
                <img :src="item.avatar" alt="" class="rounded-full bg-gray-800 h-8 w-8" />
                <div class="font-medium text-sm text-white leading-6 truncate hidden sm:block">{{ item.name }}</div>
              </a>
            </td>
            <td class="py-4 pr-4 pl-0 sm:pr-8">
              <div class="flex gap-x-2">
                <div class="font-mono text-sm text-gray-400 leading-6 truncate">{{ numberFormat(item.amount) }} $QE</div>
              </div>
            </td>
            <td class="text-sm text-white py-4 pr-4 pl-0 leading-6 sm:pr-8 lg:pr-20">
              <div v-if="item.status === 'init'">{{ item.status }}</div>
              <a :href="linkToExplorer(`/tx/${item?.meta?.transactionHash}`)" v-if="item.status === 'minted'" target="_blank">{{ item.status }}</a>
              <!-- <BsBtnBlack :loading="isSending" class="ml-2" v-if="isDebug" @click="sendAIEntropy(item, '300')">Send 300 $QEEntropy</BsBtnBlack> -->
            </td>
            <!-- <td class="text-sm py-4 pr-8 pl-0 text-gray-400 leading-6 hidden md:table-cell lg:pr-20">{{ item.duration }}</td> -->
            <td class="text-right text-sm py-4 pr-4 pl-0 text-gray-400 leading-6 sm:pr-6 lg:pr-8">
              <BsTimeAgo :time="item.created_at" class="text-gray-4 whitespace-nowrap" />
            </td>
          </tr>
        </tbody>
      </table>
    </BsLoading>
  </div>
</template>
