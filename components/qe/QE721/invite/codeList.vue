<script setup lang="ts">
import { useClipboard } from "@vueuse/core";

const { codeList, isUsed, queryYourCode, isLoadingCode } = $(inviteCodeStore());
let { isShow, currentTab } = $(inviteCodeStore());
const { alertSuccess } = $(notificationStore());
onMounted(async () => {
  await queryYourCode();
});

watch($$(isUsed), queryYourCode);

const doCopy = (source) => {
  const { copy } = useClipboard({ source });
  copy(source);
  alertSuccess("Copy succeed!", () => (isShow = true));
};
</script>
<template>
  <div>
    <div class="flex pb-5 justify-end">
      <BsFormToggleAlt v-model="isUsed" class="text-white">Is Used?</BsFormToggleAlt>
    </div>
    <BsLoading :is-loading="isLoadingCode" class="w-full">
      <table class="text-center w-full whitespace-nowrap" v-if="codeList.length">
        <colgroup>
          <col class="w-3/12" />
          <col class="w-3/12" />
          <col class="w-3/12" />
          <col class="w-3/12" />
        </colgroup>
        <thead class="border-b border-white/10 text-sm text-white leading-6">
          <tr class="text-center">
            <th scope="col" class="font-semibold py-2">Network</th>
            <th scope="col" class="font-semibold py-2">Code Type</th>
            <th scope="col" class="font-semibold py-2">Invite Code</th>
            <th scope="col" class="font-semibold py-2">{{ isUsed ? "Status" : "Created At" }}</th>
          </tr>
        </thead>
        <tbody class="divide-y divide-white/5 text-white">
          <tr v-for="item in codeList" :key="item.id">
            <td class="py-4">
              {{ item.network }}
            </td>
            <td class="py-4">
              {{ item.codeType }}
            </td>
            <td class="text-right py-4 pr-4">
              {{ shortAddress(item.code) }}
              <BsBtnPlain v-if="!isUsed" class="text-xs! p-2!" @click="doCopy(item.code)">Copy</BsBtnPlain>
            </td>
            <td class="text-sm py-4 leading-6">
              <span v-if="isUsed">
                {{ item.status }}
              </span>
              <BsTimeAgo :time="item.created_at" class="flex-none text-xs" v-else />
            </td>
          </tr>
        </tbody>
      </table>
      <div v-else class="p-10">
        <button
          type="button"
          @click="currentTab = 'Buy Code'"
          class="border-dashed rounded-lg border-2 border-gray-300 text-white text-center w-full p-12 relative block hover:border-gray-400 focus:outline-none focus:ring-2 focus:ring-lime-500 focus:ring-offset-2"
        >
          <span class="font-semibold mt-2 text-sm block">Buy a new invite code</span>
        </button>
      </div>
    </BsLoading>
  </div>
</template>
