<template>
  <v-container fluid style="background-color: #f1f1f1;">
    <Desktop />
    <v-card flat color="#f1f1f1" class="my-2 mx-auto" max-width="600">
      <v-card-title>
        Recent Tweets
      </v-card-title>
    </v-card>
    <div v-if="!isFetchJamsFinished">
      <TweetSkeleton v-for="i in 3" :key="i" />
    </div>
    <Tweet v-for="(jam, i) in getJams" :key="i" :jam="jam" />
  </v-container>
</template>

<script>
// eslint-disable-next-line no-unused-vars
import { mapActions, mapGetters } from 'vuex'
import Tweet from '~/components/tweet'
import TweetSkeleton from '~/components/tweetSkeleton'
import Desktop from '~/components/login/Desktop'

export default {
  components: { Tweet, TweetSkeleton, Desktop },
  data() {
    return {
      isFetchJamsFinished: false,
    }
  },
  async created() {
    await this.fetchJams({ orderBy: [['timestamp', 'desc']] })
    this.isFetchJamsFinished = true
    await this.refreshLikesInState()
  },
  methods: {
    ...mapActions(['fetchJams', 'refreshLikesInState']),
  },
  computed: {
    ...mapGetters(['getJams']),
  },
}
</script>
