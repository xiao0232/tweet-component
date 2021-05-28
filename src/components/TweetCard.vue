<template>
  <div ref="tweet" class="tweet-card" ></div>
</template>

<script lang="ts">
import { ref, defineComponent, onMounted, nextTick, watch } from "vue"

export default defineComponent({
  name: "TweetCard",
  props: {
    tweet_id: {
      type: String,
      required: true
    }
  },
  setup: (props) => {
    const tweet = ref<HTMLElement>()

    const initScript = () => {
      const script = document.createElement("script")
      script.setAttribute("src", "https://platform.twitter.com/widgets.js")
      script.setAttribute('async', 'true')
      script.addEventListener("load", () => render())
      document.body.appendChild(script)
    }
    const render = () => {
      if (!(<any>window).twttr) {
        initScript()
        return
      }
      
      (<any>window).twttr
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
        })
    }

    onMounted(() => {
      render()
    })
    watch(props, () => {
      render()
    })
    
    return { tweet }
  }
})
</script>

<style>
.tweet-card{
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
