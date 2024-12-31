<script setup lang="ts">
const { loadGrid, isGridDataLoading, loadMintedData, gridDataMap } = $(ixoQE721Store());
const { isLogin } = $(supabaseStore());
const {
  doLogin,
  getSigFromServer,
  writeContract,
  chain,
  address,
  currency,
  gasBalance,
  network,
  updateUserBalance,
  isUpdatingUserBalance,
  bstSwapBalance,
  bstEntropyBalance,
} = $(rwaAuthStore());

const { payTokenList, payBy, payment, ensurePaymentBalanceAndAllowance, queryBstBalance } = $(appStore());
const { alertError, addLoading, alertSuccess } = $(notificationStore());

const tokenMeta = $(inject("tokenMeta"));
const avatar = $computed(() => tokenMeta.avatar || "");

let gridRangeId = $ref(0);
let isSub = $ref(false);
const itemsMap = $computed(() => {
  const key = `${tokenMeta.tokenId}-${gridRangeId}`;
  return gridDataMap[key] || {};
});

watchEffect(async () => {
  if (isSub === false || gridRangeId == 0) return;

  await loadGrid(tokenMeta.tokenId, gridRangeId);
});

const goToGrid = (gridId) => {
  if (gridId === 0) {
    isSub = false;
    gridRangeId = 0;
    return;
  }
  isSub = true;
  gridRangeId = gridId;
};

const gridRange = (i) => {
  // 1: 0001 - 0100
  // 2: 0101 - 0200
  // 3: 0201 - 0300
  const start = usePadStart(i * 100 - 99, 4, "0");
  const end = usePadStart(i * 100, 4, "0");
  return `${start} - ${end}`;
};

const getGridId = (i) => {
  return usePadStart((gridRangeId - 1) * 100 + i, 4, "0");
};

let isShowGridModal = $ref(false);
let gridId = $ref(0);
const showGrid = (i) => {
  gridId = getGridId(i);
  isShowGridModal = true;
  if (itemsMap[gridId]) {
    // show grid information
    return;
  }
};

const { needMoreGas } = $(taskStore());
let isMintQE1155NFTLoading = $ref(false);

const doMintQE1155NFT = async () => {
  if (needMoreGas || isMintQE1155NFTLoading) {
    return;
  }
  if (!address) {
    return alertError("Your MPC Wallet is not initialized yet!");
  }

  isMintQE1155NFTLoading = true;
  const tokenId = tokenMeta.tokenId;

  // 1. check allowance for $QE
  const payAmount = parseEther(tokenMeta.nftPrice + "");

  const balanceRz = await ensurePaymentBalanceAndAllowance("IXOProtocol", payAmount);
  if (balanceRz !== true) {
    return alertError(balanceRz, () => {
      isShowGridModal = true;
      isMintQE1155NFTLoading = false;
    });
  }

  // 2. get mint sig from server
  const { data } = await getSigFromServer("/api/ixo/QE1155NFTMint", {
    tokenId,
    gridId,
    gridRangeId,
    payment,
    network,
    appaddress: getContractAddress("IXOProtocol", network),
  });
  if (data.error) {
    return alertError(data.error, () => {
      isShowGridModal = true;
      isMintQE1155NFTLoading = false;
    });
  }
  const { to, nonce, sig } = data;

  // 3. call mint func to IXOProtocol
  const loading = addLoading("Start mint $QE1155 NFT, be patient!");
  let transactionHash = "";
  try {
    const nftTokenId = tokenId * 10 ** 10 + parseInt(gridId);
    console.log(`====> nftTokenId :`, nftTokenId);
    const { tx } = await writeContract("IXOProtocol", "mintQE1155NFT", {}, to, nftTokenId, payment, payAmount, nonce, sig);
    transactionHash = tx.transactionHash;
  } catch (err) {
    isMintQE1155NFTLoading = false;
    console.log(`====> err :`, err, Object.keys(err));
    return alertError(err.shortMessage || err, false, loading);
  }

  const { data: mintedData } = await usePost("/api/ixo/QE1155NFTMinted", { transactionHash, network, tokenId, gridId });
  if (mintedData?.error) {
    isMintQE1155NFTLoading = false;
    console.log(`====> mintedData :`, mintedData);
    return alertError(mintedData.error.message, false, loading);
  }
  alertSuccess(
    "Mint $QE1155 NFT Succeed!",
    async () => {
      await loadGrid(tokenMeta.tokenId, gridRangeId);
      await loadMintedData(tokenMeta.tokenId, true);

      isMintQE1155NFTLoading = false;
      isShowGridModal = false;
      await queryBstBalance();
    },
    loading
  );
};
</script>

<template>
  <div items-center>
    <div w-full text-center>
      <span text-rainbow text-5xl class="animate-pulse">{{ tokenMeta.name }} 10K NFT Grid</span>
    </div>
    <h2 text-white py-10 flex-bc>
      <template v-if="isSub">
        <div flex-bc cursor-pointer @click="goToGrid(0)">
          <div class="h-5 mr-2 w-5 i-heroicons-arrow-left-16-solid" />
          Back
        </div>
        <div>
          Grid Range: <span text-green font-bold text-xl> {{ gridRange(gridRangeId) }}</span>
        </div>
      </template>
    </h2>
    <div>
      <div text-white text-center text-2xl md:hidden>Check on the desktop browser <br />to see the NFT grid.</div>
      <BsLoading :isLoading="isGridDataLoading" v-if="isSub">
        <div w-full h-100vh grid-cols-10 gap-1 hidden md:grid>
          <div v-for="i in 100" class="cursor-pointer group" @click="showGrid(i)">
            <BsBoxImg
              v-if="avatar"
              v-motion-pop
              v-motion-pop-visible
              v-motion-slide-visible-bottom
              v-motion-roll-visible-bottom
              :src="avatar"
              alt=""
              class="rounded-xl flex-none h-full bg-gray-800 w-full group-hover:hidden"
            />
            <div class="bg-green rounded-xl h-full text-white hidden group-hover:(flex items-center justify-center) ">{{ getGridId(i) }}</div>
          </div>
        </div>
      </BsLoading>
      <div v-else w-full h-100vh grid-cols-10 gap-1 hidden md:grid>
        <div v-for="i in 100" class="cursor-pointer group" @click="goToGrid(i)">
          <BsBoxImg
            v-if="avatar"
            v-motion-pop
            v-motion-pop-visible
            v-motion-slide-visible-bottom
            v-motion-roll-visible-bottom
            :src="avatar"
            alt=""
            class="rounded-xl flex-none h-full bg-gray-800 w-full group-hover:hidden"
          />
          <div class="bg-green rounded-xl h-full text-white hidden group-hover:(flex items-center justify-center) ">{{ gridRange(i) }}</div>
        </div>
      </div>
    </div>

    <BsDialogDefault :show="isShowGridModal" :no-padding="true" @close="isShowGridModal = false">
      <div class="bg-lime-600 py-6 px-3 shadow-2xl relative isolate overflow-hidden sm:rounded-3xl sm:px-10">
        <div flex py-5>
          <div>
            <BsBoxImg
              v-if="avatar"
              v-motion-pop
              v-motion-pop-visible
              v-motion-slide-visible-bottom
              v-motion-roll-visible-bottom
              :src="avatar"
              alt=""
              class="rounded-xl flex-none bg-gray-800 h-80 w-80 group-hover:hidden"
            />
            <!-- <div text-gray-3 text-sm text-center pt-4>Click to replace Grid NFT Image</div> -->
          </div>
          <div flex-1 pl-8 text-white text-sm text-right flex flex-col justify-between>
            <h2 class="flex-bc font-bold flex-1 tracking-tight py-2 text-2xl items-start">
              <span text-white pr-50>{{ tokenMeta.name }}</span>
              <span text-rainbow animate-pulse text-2xl> #{{ gridId }} </span>
            </h2>
            <div space-y-3>
              <div flex-bc><span text-gray-3 text-lg>Mint Price</span> {{ tokenMeta.nftPrice }} $QE</div>
              <div flex-bc>
                <span text-gray-3 text-lg>Pay By</span>
                <BsFormSelect id="payBy" v-model="payBy" :list="payTokenList" class="" />
              </div>
              <div flex-bc>
                <div flex-bc>
                  <span text-gray-3 text-lg mr-2>Balance</span>
                  <span v-if="payBy === '$QESwap'"
                    >[ <NuxtLink :to="`/bridge?t=${network}`" target="_blank" class="text-red">Deposit More</NuxtLink> ]</span
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
                <label for="currentBalance" class="text-lg text-gray-3">Gas Balance:</label>
                <div flex-cc>
                  <span font-bold mr-2> {{ numberFormat(gasBalance) }} {{ currency }}</span>
                  <BsLoadingIcon v-if="isUpdatingUserBalance" />
                  <span v-else i-material-symbols-light-directory-sync cursor-pointer w-5 h-5 @click="updateUserBalance">Reload</span>
                </div>
              </div>
              <BsGasFullfillAlert :chain="chain"></BsGasFullfillAlert>
              <div pt-5>
                <BsBtnBlack :isLoading="isMintQE1155NFTLoading" class="border-none rounded-full" @click="doMintQE1155NFT">
                  <span> Mint Now </span>
                  <span class="h-5 ml-2 w-5 i-heroicons-arrow-small-right-solid"></span>
                </BsBtnBlack>
              </div>
            </div>
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
