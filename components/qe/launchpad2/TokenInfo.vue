<script setup lang="ts">
const tokenData = $(inject("tokenData"));
const tokenMeta = $(inject("tokenMeta"));
const { isLoading } = $(ixoQE721Store());

const avatar = $computed(() => tokenMeta.avatar || "");
const website = $computed(() => tokenMeta.website || "");
const twitter = $computed(() => tokenMeta.twitter || "");
const discord = $computed(() => tokenMeta.discord || "");
</script>
<template>
  <BsLoading class="py-20" :isLoading="isLoading">
    <div class="flex-col flex space-y-10 mb-10 px-10 justify-between place-items-stretch sm:(flex-row px-0 space-y-0)">
      <BsBoxImg :src="avatar" alt="" class="rounded-xl flex-none bg-gray-800 h-70 mr-10 w-70" />
      <div flex-1 text-white flex flex-col justify-between space-y-3>
        <div flex-bc>
          <h2 text-4xl font-bold>{{ tokenMeta.name }}</h2>
          <div flex-cc space-x-3>
            <a v-if="website" target="_blank" flex-cc :href="website" class="hover:text-lime-600">
              <span i-material-symbols-house h-8 w-8 />
            </a>
            <a v-if="twitter" target="_blank" flex-cc :href="`https://x.com/${twitter}`" class="hover:text-lime-600">
              <span i-fa6-brands-x-twitter h-6 w-6 />
            </a>
            <a v-if="discord" target="_blank" flex-cc :href="discord" class="hover:text-lime-600">
              <span i-tabler-brand-discord-filled h-7 w-7 />
            </a>
          </div>
        </div>
        <p class="flex-1">
          {{ tokenMeta.desc }}
        </p>
        <QeLaunchpad2TokenInfoStats />
      </div>
    </div>
  </BsLoading>
</template>
