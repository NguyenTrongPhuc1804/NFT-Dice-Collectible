<template>
  <div class="pt-12 text-center">
    <p v-if="walletStore.address != ''">
      Your wallet address is: {{ walletStore.address }}
    </p>
    <p v-else>You've not connected your wallet yet</p>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

import { useWalletStore } from '../stores/wallet'

export default defineComponent({
  setup() {
    const walletStore = useWalletStore()

    return {
      walletStore,
    }
  },
})
</script>
