<template>
  <div class="tweet-demo">
    <button @click="changeId">change</button>
    <TweetCard :tweet_id="tweet_id" />
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue'
import TweetCard from './TweetCard.vue'

export default defineComponent({
  name: 'HelloWorld',
  components: {
    TweetCard
  },
  setup() {
    const tweet_id = ref("1396663493856841735")
    const changeId = () => {
      tweet_id.value = tweet_id.value == "1396663493856841735" ? "1398081588273979393" : "1396663493856841735"
    }
    return { tweet_id, changeId }
  }
})
</script>

<style>
.tweet-demo {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
</style>
