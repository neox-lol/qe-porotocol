<script setup lang="ts">

const popLeft = i => {
  return {
    initial: { opacity: 0, scale: 2, x: -200 * i },
    enter: { opacity: 1, x: 0, scale: 1, },
    visible: { opacity: 1, x: 0, scale: 1, },
    hovered: { scale: 1.5 },
  }
}

const popRight = i => {
  return {
    initial: { opacity: 0, scale: 2, x: 200 * i },
    enter: { opacity: 1, x: 0, scale: 1, },
    visible: { opacity: 1, x: 0, scale: 1, },
    hovered: { scale: 1.5 },
  }
}

</script>
<template>
  <div class="mx-auto mb-28 max-w-7xl px-6 sm:mb-56 lg:px-8">
    <div class="mx-auto text-center max-w-2xl" v-motion-pop-visible>
      <h2 class="font-semibold text-base text-lime-400 leading-7">We use</h2>
      <p class="font-bold mt-2 text-white tracking-tight text-3xl sm:text-4xl">The world’s most innovative tech</p>
    </div>
    <div class="flex-cc mx-auto max-w-lg mt-16 text-white gap-x-8 gap-y-15 items-center sm:max-w-xl sm:mt-20 sm:grid sm:gap-x-10 sm:grid-cols-2 lg:max-w-none  lg:mx-0 lg:mt-24 lg:grid-cols-3">
      <a href="https://eips.ethereum.org/EIPS/eip-2535" target="_blank" @vue:mounted="(node) => useMotion(node.el, popLeft(1))" class="flex object-contain col-span-1 items-center justify-center">
        <span text-5xl font-bold ml-2>EIP2535</span>
      </a>

      <a href="https://nuxt.com/" target="_blank" @vue:mounted="(node) => useMotion(node.el, popLeft(2))" class="flex object-contain col-span-1 items-center justify-center">
        <svg xmlns="http://www.w3.org/2000/svg" w-auto max-h-12 viewBox="0 0 24 24">
          <path fill="currentColor" d="M13.464 19.83h8.922c.283 0 .562-.073.807-.21a1.59 1.59 0 0 0 .591-.574a1.53 1.53 0 0 0 .216-.783a1.529 1.529 0 0 0-.217-.782L17.792 7.414a1.59 1.59 0 0 0-.591-.573a1.652 1.652 0 0 0-.807-.21c-.283 0-.562.073-.807.21a1.59 1.59 0 0 0-.59.573L13.463 9.99L10.47 4.953a1.591 1.591 0 0 0-.591-.573a1.653 1.653 0 0 0-.807-.21c-.284 0-.562.073-.807.21a1.591 1.591 0 0 0-.591.573L.216 17.481a1.53 1.53 0 0 0-.217.782c0 .275.074.545.216.783a1.59 1.59 0 0 0 .59.574c.246.137.525.21.808.21h5.6c2.22 0 3.856-.946 4.982-2.79l2.733-4.593l1.464-2.457l4.395 7.382h-5.859Zm-6.341-2.46l-3.908-.002l5.858-9.842l2.923 4.921l-1.957 3.29c-.748 1.196-1.597 1.632-2.916 1.632z" />
        </svg>
        <span text-5xl font-bold ml-2>NUXT3</span>
      </a>
      <a href="https://viem.sh/" target="_blank" @vue:mounted="(node) => useMotion(node.el, popLeft(3))" class="flex object-contain col-span-1 items-center">
        <svg w-full max-h-12 viewBox="0 0 615 224" xmlns="http://www.w3.org/2000/svg">
          <path
            d="M83.3 220.4L135.66 96.98C142.8 79.64 145.52 77.94 160.14 77.94V70.8H107.1V77.94C120.7 77.94 127.16 78.62 127.16 85.76C127.16 88.48 126.48 91.88 124.44 96.98L94.18 172.46L61.54 95.96C59.84 91.2 58.82 87.8 58.82 85.42C58.82 78.62 65.28 77.94 76.84 77.94V70.8H1.02V77.94C14.96 77.94 17 80.66 23.8 95.62L81.26 220.4H83.3ZM171.915 22.52C171.915 34.08 181.775 43.26 193.335 43.26C204.895 43.26 214.415 34.08 214.415 22.52C214.415 10.62 204.895 1.77999 193.335 1.77999C181.775 1.77999 171.915 10.62 171.915 22.52ZM175.995 96.3V191.5C175.995 208.16 172.595 209.86 157.295 209.86V217H231.075V209.86C215.775 209.86 212.375 208.16 212.375 191.5V70.8H157.295V77.94C172.595 77.94 175.995 79.64 175.995 96.3ZM298.103 76.58C316.123 76.58 324.623 93.92 325.643 118.06H264.783C267.503 90.86 280.423 76.58 298.103 76.58ZM359.303 187.76L354.883 183.68C345.703 195.92 334.483 201.36 320.203 201.36C287.223 201.36 264.103 171.44 264.103 130.3C264.103 128.94 264.103 127.58 264.103 126.56H356.923C356.923 98.34 338.223 67.4 299.123 67.4C263.763 67.4 229.763 101.06 229.763 145.94C229.763 189.8 262.743 220.4 302.863 220.4C324.623 220.4 346.043 209.18 359.303 187.76ZM434.132 209.86C418.832 209.86 415.432 208.16 415.432 191.5V104.8C421.212 93.92 430.732 86.78 442.292 86.78C459.972 86.78 468.812 98.34 468.812 122.82V191.5C468.812 208.16 465.412 209.86 450.112 209.86V217H523.892V209.86C508.252 209.86 504.852 208.16 504.852 191.5V117.04C504.852 113.64 504.512 109.9 504.172 106.84C508.932 95.96 519.132 86.78 531.712 86.78C549.732 86.78 558.572 98.34 558.572 122.82V191.5C558.572 208.16 555.172 209.86 539.872 209.86V217H613.652V209.86C598.012 209.86 594.612 208.16 594.612 191.5V117.04C594.612 89.84 581.692 67.4 550.752 67.4C525.932 67.4 509.272 86.44 503.152 100.38C498.392 81.34 485.472 67.4 460.992 67.4C438.212 67.4 422.232 83.72 415.432 97.32V70.8H360.352V77.94C375.652 77.94 379.052 79.64 379.052 96.3V191.5C379.052 208.16 375.652 209.86 360.352 209.86V217H434.132V209.86Z"
            fill="#fff" />
        </svg>
      </a>
      <a href="https://eips.ethereum.org/EIPS/eip-20" target="_blank" @vue:mounted="(node) => useMotion(node.el, popRight(1))" class="flex object-contain col-span-1 items-center justify-center">
        <span text-5xl font-bold ml-2>EIP20</span>
      </a>
      <a href="https://eips.ethereum.org/EIPS/eip-721" target="_blank" @vue:mounted="(node) => useMotion(node.el, popRight(2))" class="flex object-contain col-span-1 items-center justify-center">
        <span text-5xl font-bold ml-2>EIP721</span>
      </a>
      <a href="https://eips.ethereum.org/EIPS/eip-1155" target="_blank" @vue:mounted="(node) => useMotion(node.el, popRight(3))" class="flex object-contain col-span-1 items-center justify-center">
        <span text-5xl font-bold ml-2>EIP1155</span>
      </a>
    </div>
  </div>
</template>