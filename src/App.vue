<template>
  <img alt="Vue logo" src="./assets/logo.png" />
  <TweetDemo />
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import TweetDemo from './components/TweetDemo.vue'

export default defineComponent({
  name: 'App',
  components: {
    TweetDemo
  }
})
</script>

<style>
body {
  background-color: #2c3e50;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
