<template>
  <div class="tweet-card">
    <div v-if="isLoading" class="skeleton-screen" >
    <!-- <div class="skeleton-screen" > -->
      <div class="skeleton-circle" ></div>
      <div class="skeleton-screen-name" ></div>
      <div class="skeleton-screen-id" ></div>
      <div class="skeleton-text-1" ></div>
      <div class="skeleton-text-2" ></div>
      <div class="skeleton-text-3" ></div>
      <div class="skeleton-text-4" ></div>
      <div class="skeleton-time" ></div>
      <div class="skeleton-hr" ></div>
      <div class="skeleton-footer" ></div>
    </div>
    <div ref="tweet" class="tweet-card" ></div>
  </div>
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
      
      isLoading.value = true;
      
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
              isLoading.value = false
            })
            .finally(() => {
              isLoading.value = false;
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

<style>
.tweet-card{
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

.skeleton-screen {
  display: block;
  width: 550px;
  height: 300px;
  margin: 10px auto;
  border-radius: 12px;
  background-color: #a7a7a7;
  position: relative;
  overflow: hidden
}

.skeleton-circle {
  width: 48px;
  height: 48px;
  margin: 10px auto;
  border-radius: 50%;
  background-color: #d9d9d9;
  position: absolute;
  top: 12px;
  left: 16px;
  overflow: hidden
}
.skeleton-circle:before {
  content: '';
  display: block;
  height: 100%;
  width: 100%;
  background: linear-gradient(to right, transparent, rgba(255, 255, 255, .5), transparent);
  animation: skeleton-animation 1.2s linear infinite;
}
.skeleton-screen-name {
  width: 140px;
  height: 14px;
  margin: 10px auto;
  background-color: #d9d9d9;
  position: absolute;
  top: 18px;
  left: 68px;
  overflow: hidden
}
.skeleton-screen-name:before {
  content: '';
  display: block;
  height: 100%;
  width: 100%;
  background: linear-gradient(to right, transparent, rgba(255, 255, 255, .5), transparent);
  animation: skeleton-animation 1.2s linear infinite;
}
.skeleton-screen-id {
  width: 100px;
  height: 14px;
  margin: 10px auto;
  background-color: #d9d9d9;
  position: absolute;
  top: 38px;
  left: 68px;
  overflow: hidden
}
.skeleton-screen-id:before {
  content: '';
  display: block;
  height: 100%;
  width: 100%;
  background: linear-gradient(to right, transparent, rgba(255, 255, 255, .5), transparent);
  animation: skeleton-animation 1.2s linear infinite;
}
.skeleton-text-1 {
  width: 515px;
  height: 14px;
  margin: 10px auto;
  background-color: #d9d9d9;
  position: absolute;
  top: 80px;
  left: 16px;
  overflow: hidden
}
.skeleton-text-1:before {
  content: '';
  display: block;
  height: 100%;
  width: 100%;
  background: linear-gradient(to right, transparent, rgba(255, 255, 255, .5), transparent);
  animation: skeleton-animation 1.2s linear infinite;
}
.skeleton-text-2 {
  width: 515px;
  height: 14px;
  margin: 10px auto;
  background-color: #d9d9d9;
  position: absolute;
  top: 104px;
  left: 16px;
  overflow: hidden
}
.skeleton-text-2:before {
  content: '';
  display: block;
  height: 100%;
  width: 100%;
  background: linear-gradient(to right, transparent, rgba(255, 255, 255, .5), transparent);
  animation: skeleton-animation 1.2s linear infinite;
}
.skeleton-text-3 {
  width: 515px;
  height: 14px;
  margin: 10px auto;
  background-color: #d9d9d9;
  position: absolute;
  top: 128px;
  left: 16px;
  overflow: hidden
}
.skeleton-text-3:before {
  content: '';
  display: block;
  height: 100%;
  width: 100%;
  background: linear-gradient(to right, transparent, rgba(255, 255, 255, .5), transparent);
  animation: skeleton-animation 1.2s linear infinite;
}
.skeleton-text-4 {
  width: 515px;
  height: 14px;
  margin: 10px auto;
  background-color: #d9d9d9;
  position: absolute;
  top: 152px;
  left: 16px;
  overflow: hidden
}
.skeleton-text-4:before {
  content: '';
  display: block;
  height: 100%;
  width: 100%;
  background: linear-gradient(to right, transparent, rgba(255, 255, 255, .5), transparent);
  animation: skeleton-animation 1.2s linear infinite;
}
.skeleton-time {
  width: 160px;
  height: 20px;
  margin: 10px auto;
  background-color: #d9d9d9;
  position: absolute;
  top: 200px;
  left: 16px;
  overflow: hidden
}
.skeleton-time:before {
  content: '';
  display: block;
  height: 100%;
  width: 100%;
  background: linear-gradient(to right, transparent, rgba(255, 255, 255, .5), transparent);
  animation: skeleton-animation 1.2s linear infinite;
}
.skeleton-hr {
  width: 515px;
  height: 2px;
  margin: 10px auto;
  background-color: #d9d9d9;
  position: absolute;
  top: 230px;
  left: 16px;
  overflow: hidden
}
.skeleton-hr:before {
  content: '';
  display: block;
  height: 100%;
  width: 100%;
  background: linear-gradient(to right, transparent, rgba(255, 255, 255, .5), transparent);
  animation: skeleton-animation 1.2s linear infinite;
}
.skeleton-footer {
  width: 515px;
  height: 32px;
  margin: 10px auto;
  background-color: #d9d9d9;
  position: absolute;
  top: 240px;
  left: 16px;
  overflow: hidden
}
.skeleton-footer:before {
  content: '';
  display: block;
  height: 100%;
  width: 100%;
  background: linear-gradient(to right, transparent, rgba(255, 255, 255, .5), transparent);
  animation: skeleton-animation 1.2s linear infinite;
}

  
@keyframes skeleton-animation {
  0% {
    transform: translateX(-100%)
  }
  100% {
    transform: translateX(100%)
  }
}
</style>
