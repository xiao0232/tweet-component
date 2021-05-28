<template>
  <div v-if="isLoading" class="skeleton-screen" >
  <!-- <div class="skeleton-screen" > -->
    <div class="skeleton skeleton__circle" ></div>
    <div class="skeleton skeleton__screen-name" ></div>
    <div class="skeleton skeleton__screen-id" ></div>
    <div class="skeleton__text__container" >
      <div class="skeleton skeleton__text" ></div>
      <div class="skeleton skeleton__text" ></div>
      <div class="skeleton skeleton__text" ></div>
      <div class="skeleton skeleton__text" ></div>
    </div>
    <div class="skeleton skeleton__time" ></div>
    <div class="skeleton skeleton__hr" ></div>
    <div class="skeleton skeleton__footer" ></div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue"

export default defineComponent({
  name: "SkeletonTweetCard",
  props: {
    isLoading: {
      type: Boolean,
      defoult: false
    }
  }
})
</script>

<style lang="scss">
.skeleton-screen {
  display: flex;
  max-width: 550px;
  min-width: 250px;
  width: 100%;
  height: 300px;
  margin: 10px auto;
  border-radius: 12px;
  background-color: #a7a7a7;
  position: relative;
  overflow: hidden;
}

.skeleton {
  margin: 10px auto;
  background-color: #d9d9d9;
  position: absolute;
  overflow: hidden;
  
  &__circle {
    width: 48px;
    height: 48px;
    border-radius: 50%;
    top: 12px;
    left: 16px;
  }
  &__screen-name {
    width: 140px;
    height: 14px;
    top: 18px;
    left: 68px;
  }
  &__screen-id {
    width: 100px;
    height: 14px;
    top: 38px;
    left: 68px;
  }
  @for $i from 1 through 4 {
    &__text:nth-of-type(#{$i}) {
      width: 515px;
      height: 14px;
      top: calc(80px + (#{$i} - 1) * 24px);
      left: 16px;
    }
  }
  &__time {
    width: 160px;
    height: 20px;
    top: 200px;
    left: 16px;
  }
  &__hr {
    max-width: 515px;
    width: calc(100% - 2 * 16px);
    height: 2px;
    top: 230px;
    left: 16px;
  }
  &__footer {
    max-width: 515px;
    width: calc(100% - 2 * 16px);
    height: 32px;
    top: 240px;
    left: 16px;
  }

  &:before {
    content: '';
    display: block;
    height: 100%;
    width: 100%;
    background: linear-gradient(to right, transparent, rgba(255, 255, 255, .5), transparent);
    animation: skeleton-animation 1s linear infinite;
  }
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
