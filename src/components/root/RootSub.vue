<template>
  <div>
    <div class="error window half-width info" id="error-window" v-if='errMsg'>
      {{ errMsg }}
    </div>
    <b-container>
      <div class='info-message gentle-message window half-width gentle-message mt-4' v-if='hasConnectedWallet'>
        {{ $t('wallet.notConnected') }}<button class="ml-2" @click='changeWallets'>{{ $t('wallet.connect') }}</button>
      </div>
    </b-container>
  </div>
</template>

<script>
  import { getters, contract as currentContract, changeContract, poolMenu } from '../../contract'
  import init, { onboard, changeWallets } from '../../init'
  import * as volumeStore from '@/components/common/volumeStore'

  export default {
    props: {
      errMsg: {
        type: String,
        default: ''
      }
    },
    methods: {
      async changeWallets() {
        changeWallets()
      },
    },
    computed: {
      ...getters,
      hasConnectedWallet() {
        return this.default_account == '0x0000000000000000000000000000000000000000' 
                && !['Donate', 'StatsDaily', 'Audits', 'Stats', 'Contracts', 'FAQ', 'RootFAQ'].includes(this.$route.name)
      },
      plsReturn() {
        return currentContract.currentContract.toLowerCase() == '0x72c20f89008729c91b6bb85f3104fda942494cef'.toLowerCase()
      },
    }
  }
</script>

<style>

</style>