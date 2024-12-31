<script setup lang="ts">
const { loadUserToken, userMintedTokenMap, isLoading, doSubmit, form, isFreeMintExceeded, basicInfoRef, valuationRef, marketingRef } = $(
  ixoQE721Store()
);

const ftTotalSupply = $computed(() => form.ftSwapUnit * form.nftTotalSupply);

const { userId } = $(supabaseStore());
const tokenIdList = $computed(() => {
  if (userMintedTokenMap[userId]) {
    return userMintedTokenMap[userId].items.map((item) => item.tokenId);
  }
  return [];
});

const currentToken = $computed(() => {
  if (!userMintedTokenMap[userId]) return {};
  const token = userMintedTokenMap[userId].items.filter((item) => item.tokenId === form.tokenId);
  return token[0];
});

watchEffect(async () => {
  if (!userId) return;
  if (userMintedTokenMap[userId]) return;

  await loadUserToken(userId);
  if (tokenIdList[0]) {
    form.tokenId = tokenIdList[0];
  }
});

const canSubmit = $computed(() => {
  return tokenIdList.length > 0 && !isFreeMintExceeded;
});

const buyType = $computed(() => currentToken.meta.buyType);

const isSBT = $computed(() => {
  if (!form.tokenId) return false;

  const sbtBuyTypeArr = ["X.com", "Pump.Fun"];
  if (sbtBuyTypeArr.includes(buyType)) return true;

  return false;
});

watchEffect(() => {
  if (!isSBT) return;

  form.twitter = currentToken.name;
});

const totalIncome = $computed(() => numberFormat(form.nftPrice * form.nftTotalSupply));
</script>

<template>
  <BsLoading :isLoading="isLoading">
    <div class="divide-y divide-white/15">
      <div class="grid py-16 gap-x-8 gap-y-10 grid-cols-1 md:grid-cols-3" ref="basicInfoRef">
        <div>
          <h2 class="font-semibold text-base text-white leading-7">Basic Information</h2>
          <p class="mt-1 text-sm text-gray-400 leading-6">Some basic metadata for your $QE1155.</p>
        </div>
        <div class="md:col-span-2">
          <div class="grid gap-x-6 gap-y-8 grid-cols-1 sm:max-w-2xl sm:grid-cols-6">
            <div class="col-span-full">
              <label for="twitter" class="flex-bc font-medium text-sm text-white leading-6">
                <span>Token ID</span>
                <span class="text-red" v-if="isSBT">It's a SBT ({{ buyType }} Sale)</span>
              </label>
              <div class="mt-2">
                <BsFormSelect v-if="tokenIdList.length" id="tokenId" v-model="form.tokenId" :list="tokenIdList" isDark />
                <div class="flex-bc text-red" v-else>
                  You do not have any $QE721 NFT yet, pls mint first
                  <NuxtLink
                    class="bg-rainbow cursor-pointer flex py-3 w-40 justify-center items-center border-none! font-bold! rounded-2xl! hover:(animate-pulse)"
                    to="/launchpad#price"
                    >Go For Mint Now
                  </NuxtLink>
                </div>
              </div>
            </div>
            <div class="col-span-full">
              <label for="twitter" class="flex-bc font-medium text-sm text-white leading-6">
                <span>Twitter</span>
                <span text-red v-if="isSBT">SBT, can not change twitter handler</span>
              </label>
              <div class="mt-2">
                <input id="twitter" name="twitter" type="url" v-model="form.twitter" :disabled="isSBT" autocomplete="twitter" class="form-input" />
              </div>
            </div>
            <div class="sm:col-span-2" id="avatar-uploader">
              <BsFormAvatarUploader v-model="form.avatar" />
            </div>
            <div class="flex flex-col justify-between sm:col-span-4">
              <div>
                <label for="name" class="font-medium text-sm text-white leading-6 block">Project Name</label>
                <div class="mt-2">
                  <input type="text" name="name" id="name" v-model="form.name" autocomplete="name" class="form-input" />
                </div>
              </div>
              <div mt-4>
                <label for="desc" class="font-medium text-sm text-white leading-6 block">Description</label>
                <div class="mt-2">
                  <resize-textarea
                    class="form-input"
                    id="desc"
                    v-model="form.desc"
                    w-full
                    placeholder="The description for your project!"
                    :rows="2"
                    :cols="5"
                  />
                </div>
              </div>
            </div>
            <div class="col-span-full">
              <label for="website" class="font-medium text-sm text-white leading-6 block">Website</label>
              <div class="mt-2">
                <input
                  id="website"
                  name="website"
                  type="url"
                  v-model="form.website"
                  autocomplete="website"
                  class="form-input"
                  placeholder="https://your-web-site.com"
                />
              </div>
            </div>
            <div class="col-span-full">
              <label for="discord" class="font-medium text-sm text-white leading-6 block">Discord invite link</label>
              <div class="mt-2">
                <input
                  id="discord"
                  name="discord"
                  type="url"
                  v-model="form.discord"
                  autocomplete="discord"
                  class="form-input"
                  placeholder="https://discord.gg/xxxx"
                />
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="grid py-16 gap-x-8 gap-y-10 grid-cols-1 md:grid-cols-3" ref="valuationRef">
        <div>
          <h2 class="font-semibold text-base text-white leading-7">Valuation and Price</h2>
          <p class="mt-1 text-sm text-gray-400 leading-6">1. FT here is the same as ERC1155 token that can be trade on any NFT marketplace.</p>
          <p class="mt-1 text-sm text-gray-400 leading-6">2. NFT here is the same as ERC721 token that can be trade on any NFT marketplace.</p>
          <p class="mt-1 text-sm text-gray-400 leading-6">
            3. $QE($QESwap only) is bridged from Polygon USDT, user can deposit / withdraw at any time.
          </p>
        </div>
        <div class="md:col-span-2">
          <div class="grid gap-x-6 gap-y-8 grid-cols-1 sm:max-w-2xl sm:grid-cols-6">
            <div class="col-span-full">
              <label for="ftTotalSupply" class="font-medium text-sm text-white leading-6 block"
                >Z <span text-gray-600>( FT Total Supply )</span></label
              >
              <div class="mt-2 sm:flex-bc">
                <div>
                  <input
                    id="ftTotalSupply"
                    name="ftTotalSupply"
                    type="text"
                    v-model="ftTotalSupply"
                    disabled
                    autocomplete="ftTotalSupply"
                    class="form-input"
                  />
                </div>
                <div flex-1 text-gray-400 mt-2 sm:mt-0 text-right>
                  <span text-white>Z</span> ({{ numberFormat(ftTotalSupply) }}) = <span text-white>X</span> ( {{ numberFormat(form.ftSwapUnit) }} ) *
                  <span text-white>Y</span> ( {{ numberFormat(form.nftTotalSupply) }} )
                </div>
              </div>
            </div>
            <div class="col-span-full">
              <label for="nftTotalSupply" class="font-medium text-sm text-white leading-6 block"
                >Y <span text-gray-600>( NFT Total Supply )</span></label
              >
              <div class="mt-2 sm:flex-bc">
                <div>
                  <input
                    id="nftTotalSupply"
                    name="nftTotalSupply"
                    type="text"
                    v-model="form.nftTotalSupply"
                    disabled
                    autocomplete="nftTotalSupply"
                    class="form-input"
                  />
                </div>
                <div flex-1 text-gray-400 mt-2 sm:mt-0 text-right>The total supply of NFT, 10K for every project.</div>
              </div>
            </div>
            <div class="col-span-full">
              <label for="ftSwapUnit" class="font-medium text-sm text-white leading-6 block">X <span text-gray-600>( FT Swap Unit ) </span></label>
              <div mt-2 sm:flex-bc>
                <div>
                  <input
                    id="ftSwapUnit"
                    name="ftSwapUnit"
                    type="text"
                    v-model="form.ftSwapUnit"
                    autocomplete="ftSwapUnit"
                    placeholder="X >= 1"
                    class="form-input"
                  />
                </div>
                <div flex-1 text-gray-400 mt-2 sm:mt-0 text-right>How many FT token can swap with 1 NFT ?</div>
              </div>
            </div>
            <div class="col-span-full">
              <label for="nftPrice" class="font-medium text-sm text-white leading-6 block">P <span text-gray-600>( NFT Price )</span></label>
              <div mt-2 sm:flex-bc>
                <div class="rounded-md shadow-sm mt-2 relative">
                  <input
                    v-model="form.nftPrice"
                    id="nftPrice"
                    name="nftPrice"
                    type="text"
                    class="form-input"
                    placeholder="0.00"
                    aria-describedby="price-currency"
                  />
                  <div class="flex pr-3 inset-y-0 right-0 pointer-events-none absolute items-center">
                    <span class="text-gray-500 sm:text-sm" id="price-currency">$QE</span>
                  </div>
                </div>
                <div flex-1 text-gray-400 mt-2 sm:mt-0 text-right>
                  <span text-white>Total Income</span> ( {{ totalIncome }} $QE ) = <span text-white>P</span> ( {{ numberFormat(form.nftPrice) }} $QE
                  ) * <span text-white>Y</span> ( {{ numberFormat(form.nftTotalSupply) }} )
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="grid py-16 gap-x-8 gap-y-10 grid-cols-1 md:grid-cols-3" ref="marketingRef">
        <div>
          <h2 class="font-semibold text-base text-white leading-7">Marketing Strategy</h2>
          <p class="mt-1 text-sm text-gray-400 leading-6"></p>
        </div>
        <div class="md:col-span-2">
          <div class="grid gap-x-6 gap-y-8 grid-cols-1 sm:max-w-2xl sm:grid-cols-6">
            <div class="col-span-full">
              <label for="inviteNewUserReward" class="font-medium text-sm text-white leading-6 block">Invite new buyers reward</label>
              <div class="mt-2 sm:flex-bc">
                <div>
                  <input
                    id="inviteNewUserReward"
                    name="inviteNewUserReward"
                    type="text"
                    v-model="form.inviteNewUserReward"
                    autocomplete="inviteNewUserReward"
                    class="form-input"
                  />
                </div>
                <div flex-1 text-gray-400 mt-2 sm:mt-0 text-right>
                  User can get {{ numberFormat(form.inviteNewUserReward) }} FT after invite 4 new users. <br />
                  These users must pay $QE to buy the NFT/FT.
                </div>
              </div>
            </div>

            <div class="col-span-full">
              <label for="freeMintAmountPerUser" class="font-medium text-sm text-white leading-6 block"
                >Retweet to free mint FT amount per user</label
              >
              <div class="mt-2 sm:flex-bc">
                <div>
                  <input
                    id="freeMintAmountPerUser"
                    name="freeMintAmountPerUser"
                    type="text"
                    v-model="form.freeMintAmountPerUser"
                    autocomplete="freeMintAmountPerUser"
                    class="form-input"
                  />
                </div>
                <div flex-1 text-gray-400 mt-2 sm:mt-0 text-right>
                  Every X user can get {{ form.freeMintAmountPerUser }} FT after they make <br />
                  a retweet to x.com (only once per X user)
                </div>
              </div>
            </div>

            <div class="col-span-full">
              <label for="retweetTags" class="font-medium text-sm text-white leading-6 block">Retweet Tags</label>
              <div class="mt-2 sm:flex-bc">
                <div>
                  <input id="retweetTags" name="retweetTags" type="text" v-model="form.retweetTags" autocomplete="retweetTags" class="form-input" />
                </div>
                <div flex-1 text-gray-400 mt-2 sm:mt-0 text-right>Seperate by comma, eg: IXOProtocol,QuantumEntanglement</div>
              </div>
            </div>

            <div class="col-span-full">
              <label for="retweetStatusLink" class="font-medium text-sm text-white leading-6 block">Retweet twitter status link</label>
              <div class="mt-2 sm:flex-bc">
                <div>
                  <input
                    id="retweetStatusLink"
                    name="retweetStatusLink"
                    type="url"
                    v-model="form.retweetStatusLink"
                    autocomplete="retweetStatusLink"
                    class="w-80 form-input"
                    placeholder="https://x.com/your-status-link"
                  />
                </div>
                <div flex-1 text-gray-400 mt-2 sm:mt-0 text-right>
                  User require to retweet the status <br />
                  to get free mint, eg:
                  <a text-red target="_blank" href="https://x.com/QuantumEntanglement/status/1742048665827779026">QuantumEntanglement Example</a>
                </div>
              </div>
            </div>

            <div class="col-span-full">
              <label for="freeMintUserAmount" class="font-medium text-sm text-white leading-6 block">FT Free mint max user amount</label>
              <div class="mt-2 sm:flex-bc">
                <div>
                  <input
                    id="freeMintUserAmount"
                    name="freeMintUserAmount"
                    type="text"
                    v-model="form.freeMintUserAmount"
                    autocomplete="freeMintUserAmount"
                    class="form-input"
                  />
                </div>
                <div flex-1 text-gray-400 mt-2 sm:mt-0 text-right>
                  Up to {{ numberFormat(form.freeMintUserAmount * form.freeMintAmountPerUser) }} FT will be free minted

                  <span v-if="isFreeMintExceeded" class="text-red"
                    ><br />
                    {{ numberFormat(form.freeMintUserAmount * form.freeMintAmountPerUser) }} Exceed your total FT supply
                    {{ numberFormat(form.ftSwapUnit * form.nftTotalSupply) }}</span
                  >
                </div>
              </div>
            </div>
          </div>
          <div class="flex-cc mt-8 sm:flex-bc">
            <BsBtnIndigo class="w-full sm:w-auto" @click="doSubmit" :disabled="!canSubmit">Submit</BsBtnIndigo>
          </div>
        </div>
      </div>
    </div>
  </BsLoading>
</template>
