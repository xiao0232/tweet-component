<template>
  <div class="tweet-card">
    <SkeletonTweetCard :isLoading="isLoading" />
    <div ref="tweet" class="tweet-card"></div>
  </div>
</template>

<script lang="ts">
import { ref, defineComponent, onMounted, nextTick, watch } from "vue"
import SkeletonTweetCard from "./SkeletonTweetCard.vue"

export default defineComponent({
  name: "TweetCard",
  components: {
    SkeletonTweetCard
  },
  props: {
    tweet_id: {
      type: String,
      required: true
    }
  },
  setup: (props) => {
    const isLoading = ref(true)
    const tweet = ref<HTMLElement>()

    const initScript = () => {
      const script = document.createElement("script")
      script.setAttribute("src", "https://platform.twitter.com/widgets.js")
      script.setAttribute('async', 'true')
      script.addEventListener("load", () => render())
      document.body.appendChild(script)
    }
    const render = async () => {
      if (!(<any>window).twttr) {
        initScript()
        return
      }
      
      isLoading.value = true
      
      await (<any>window).twttr
        .ready()
        .then(({ widgets }: any) => {
          if (tweet.value) {
            tweet.value.innerHTML = ""
          }
          widgets
            .createTweet(props.tweet_id, tweet.value)
            .then(() => {
              nextTick()
            })
            .finally(() => {
              isLoading.value = false
            })
        })
        
    }

    onMounted(() => {
      render()
    })
    watch(props, () => {
      render()
    })
    
    return { tweet, isLoading }
  }
})
</script>

<style lang="scss">
.tweet-card{
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
</style>
