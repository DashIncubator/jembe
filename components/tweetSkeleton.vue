<template>
  <v-card class="my-2 mx-auto" max-width="600">
    <v-skeleton-loader
      max-width="300"
      type="list-item-avatar-two-line"
    ></v-skeleton-loader>

    <v-card-text class="subtitle-1">
      <v-skeleton-loader max-width="300" type="text"></v-skeleton-loader>
      <v-skeleton-loader max-width="100" type="text"></v-skeleton-loader>
    </v-card-text>

    <v-card-actions @click="showLoginNag()">
      <v-list-item class="grow">
        <v-row align="center" justify="end">
          <v-btn text disabled="">Follow </v-btn>
          <v-spacer />
          <v-icon class="mr-1">mdi-twitter-retweet</v-icon>
          <span class="subheading mr-2">3</span>
          <span class="mr-1">·</span>
          <v-icon class="mr-1" disabled="">'mdi-heart-outline' </v-icon>
          <span class="subheading mr-2">0</span>
          <span class="mr-1">·</span>
          <v-icon class="mr-1" disabled="">$dash </v-icon>
          <span class="mr-1">·</span>
          <v-icon class="mr-1">mdi-share-variant</v-icon>
          <span class="subheading">45</span>
        </v-row>
      </v-list-item>
    </v-card-actions>
  </v-card>
</template>
<script>
export default {
  name: 'TweetSkeleton',
}
</script>
