<script setup lang="ts">
const { alertError, alertSuccess, addLoading } = $(notificationStore());
const { name, isLogin, shareLink } = $(supabaseStore());
const { doLogin, update, toggle, address, getSigFromServer, network, writeContract } = $(rwaAuthStore());
const { loadRewardItems } = $(ixoStore());

onMounted(() => {
  const redirectPath = `${location.origin}${location.pathname}?showModal=yes`;
  update("redirectPath", redirectPath);
});

let isShow = $ref(false);
let isShowGasDialog = $ref(false);
let isShowLinkInput = $ref(false);

const mintJson = encodeURIComponent(`
{  
  "p": "#XRC20",
  "op": "mint",
  "tick": "XRC20",
  "max": "210000000000",
  "amt": "1000",
  "by": "${name}"
}`);
const text = $computed(() => `Follow @QuantumEntanglement, RT and LIKE via ${shareLink} to get your 1k $QE${mintJson}`);

const { needMoreGas } = $(taskStore());
const shareTweetStatusLink = "https://twitter.com/QuantumEntanglement/status/1742048665827779026";
const tags = "XRC20,RWAWallet";
const twitterShareBtnLink = $computed(() => {
  return `https://twitter.com/intent/tweet?text=${text}&url=${shareTweetStatusLink}&hashtags=${tags}`;
});
let isLoading = $ref(false);
let link = $ref("");

const doSaveRetweetLink = async () => {
  if (needMoreGas) {
    isShowGasDialog = true;
    return;
  }
  if (!address) {
    return alertError("Your MPC Wallet is not initialized yet!");
  }

  if (name !== link.split("/")[3]) {
    return alertError("Twitter Handler and Retweet status link is not the same twitter account!");
  }

  isLoading = true;
  const { data } = await getSigFromServer("/api/ixo/xrc20Retweet", { link, network, appaddress: getContractAddress("IXOProtocol", network) });
  if (data.status === "minted") {
    isLoading = false;
    return alertError("You already mint the reward");
  }

  const { to, amount, nonce, sig } = data;
  const loading = addLoading("Start mint 1000 $QE, be patient!");
  let transactionHash = "";
  try {
    const { tx } = await writeContract("IXOProtocol", "mintXRC20", {}, to, parseEther(amount.toString()), nonce, sig);
    transactionHash = tx.transactionHash;
  } catch (err) {
    isLoading = false;
    return alertError(err.shortMessage, false, loading);
  }

  const { data: mintedData } = await usePost("/api/ixo/xrc20RetweetMinted", { transactionHash, network });
  if (mintedData?.error) {
    isLoading = false;
    return alertError(mintedData.error.message, false, loading);
  }
  alertSuccess(
    "Mint 1000 $QE20 Succeed!",
    async () => {
      await loadRewardItems("xrc20");
      isLoading = false;
      isShow = false;
    },
    loading
  );
};
</script>

<template>
  <div flex justify="center">
    <BsBtnDefault
      v-motion-slide-bottom
      v-motion-slide-visible-top
      @click="isShow = true"
      class="bg-rainbow flex my-20 py-3 w-80 justify-center items-center border-none! font-bold! rounded-2xl! text-xl! hover:(scale-120 animate-pulse) "
    >
      <span i-noto-backhand-index-pointing-right w-5 h-5 mr-2 flex />
      Start Mint
    </BsBtnDefault>
    <BsDialogDefault :show="isShow" :no-padding="true" @close="isShow = false">
      <div class="bg-lime-600 max-w-2xl py-6 px-3 shadow-2xl relative isolate overflow-hidden sm:rounded-3xl sm:px-12 xl:py-8">
        <h2 class="font-bold mx-auto my-10 text-center text-white text-xl tracking-tight max-w-2xl sm:text-2xl">
          Tweet to Mint Your First
          <br />
          <br />
          <span text-rainbow uppercase text-6xl animate-pulse> 1k $QE20 </span>
        </h2>
        <div flex-cc>
          <BsBtnBlack v-if="!isLogin" @click="doLogin('twitter', toggle)" rounded-full>
            <span i-ci-twitter mr-1></span>
            Auth with Twitter
          </BsBtnBlack>
          <div v-else flex flex-col items-center w-full>
            <a
              target="_blank"
              :href="twitterShareBtnLink"
              @click="isShowLinkInput = true"
              class="bg-black rounded-full m-2 text-sm py-3 px-6 text-gray-100 inline-flex items-center hover:opacity-60"
              title="Click to tweet"
            >
              <span i-ci-twitter mr-1></span>
              Click to Tweet!
            </a>
            <BsLoading v-if="isShowLinkInput" :is-loading="isLoading">
              <div class="rounded-xl flex flex-col space-y-3 border-1 mt-10 w-full py-8 px-6">
                <input
                  id="tweet-status-link"
                  v-model="link"
                  name="tweet-status-link"
                  type="url"
                  autocomplete="tweet-status-link"
                  required="true"
                  class="rounded-md bg-white/5 border-0 shadow-sm ring-inset text-white w-sm py-2 px-3.5 ring-1 ring-white/10 sm:text-sm sm:leading-6 focus:ring-inset focus:ring-white focus:ring-2"
                  placeholder="Enter your tweet status link"
                />
                <button
                  @click="doSaveRetweetLink"
                  class="bg-white rounded-md flex-none font-semibold shadow-sm text-sm py-2.5 px-3.5 text-gray-900 hover:bg-gray-100 focus-visible:outline focus-visible:outline-white focus-visible:outline-2 focus-visible:outline-offset-2"
                >
                  Submit
                </button>
              </div>
            </BsLoading>
            <div v-else text-gray-400 text-base pt-10 leading-4>After you send out the tweet, remember to copy the status link back here!</div>
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
    <QeQE20DepositGasDialog :show="isShowGasDialog" @close="isShowGasDialog = false" />
  </div>
</template>
