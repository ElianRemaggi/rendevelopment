<script setup>
//saturate-150 contrast-100'

import { VueLenis, useLenis } from 'lenis/vue'
import { watch } from 'vue'

const lenis = useLenis(({ scroll }) => {
  // called every scroll

})

watch(lenis, (lenis) => {
  // lenis instance
})

</script>

<template>

  <div class="relative font-mono min-h-screen-2000 min-h-[2000px]">

    <div class="fixed inset-0 -z-10 bg-[url('@/assets/cover.png')] bg-cover bg-center filter hue-rotate-1" />

    <VueLenis root>
      <div class="relative">
        <NuxtRouteAnnouncer />
        <NuxtPage />
      </div>
    </VueLenis>
  </div>

</template>