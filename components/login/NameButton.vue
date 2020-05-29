<template>
  <div>
    <v-btn
      v-if="$store.state.onboardType !== 'createAccount'"
      style="
        border-top-left-radius: 13px;
        border-bottom-right-radius: 13px;
        border-top-right-radius: 1px;
        border-bottom-left-radius: 1px;
      "
      large
      class="ml-2 mb-4"
      color="primary"
      :disabled="!this.$store.state.name.isValid"
      :loading="isLoading"
      @click="onboardMe()"
    >
      {{ this.$store.state.onboardText }}
    </v-btn>
    <v-btn
      v-if="$store.state.onboardType === 'createAccount'"
      style="
        border-top-left-radius: 13px;
        border-bottom-right-radius: 13px;
        border-top-right-radius: 1px;
        border-bottom-left-radius: 1px;
      "
      large
      class="ml-2 mb-4"
      color="primary"
      :href="deeplink"
      target="_blank"
    >
      {{ this.$store.state.onboardText }}
    </v-btn>
    <span v-if="isLoading">
      {{ this.$store.getters.getLoadingStep }}
    </span>
  </div>
</template>

<script>
import { mapActions } from 'vuex'
const sleep = (ms) => new Promise((resolve) => setTimeout(resolve, ms))

export default {
  components: {},
  data() {
    return {
      isLoading: false,
    }
  },
  computed: {
    deeplink() {
      return `http://evowallet.io/#/?name=${this.$store.state.name.label}`
    },
  },
  methods: {
    ...mapActions(['registerNameOnceBalance', 'onboard']),
    async onboardMe() {
      this.isLoading = true
      if (this.$store.state.identityId) {
        await this.onboard()
        this.isLoading = false
      } else {
        await sleep(1000)
        this.onboardMe()
      }
    },
  },
}
</script>
