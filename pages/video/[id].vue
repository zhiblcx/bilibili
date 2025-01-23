<script setup lang="ts">
import video from '@/public/video/video.mp4'
import coverImage from '@/public/video-image/cover.png'
import pauseImage from '@/assets/images/pause.png'
import { ref, watch } from 'vue'
import type { BarrageInstance } from 'vant'

const videoStatus = ref<boolean>(false)
const videoRef = ref<HTMLVideoElement | null>(null)
const barrage = ref<BarrageInstance>()

const defaultList = [
  { id: 100, text: '轻量' },
  { id: 101, text: '可定制的' },
  { id: 102, text: '移动端' },
  { id: 103, text: 'Vue' },
  { id: 104, text: '组件库' },
  { id: 105, text: 'VantUI' },
  { id: 106, text: '666' }
]

const list = ref([...defaultList])

const onPlay = () => {
  videoStatus.value = true
  videoRef.value?.play()
}

const onPause = () => {
  videoStatus.value = false
  videoRef.value?.pause()
}

watch(videoStatus, () => {
  if (videoStatus.value) {
    barrage.value?.play()
  } else {
    barrage.value?.pause()
  }
})
</script>

<template>
  <NuxtLayout name="home-layouts" />
  <div class="relative">
    <van-barrage
      :auto-play="false"
      v-model="list"
      ref="barrage"
    >
      <video
        controls
        class="w-full mt-[40px]"
        :src="video"
        :poster="coverImage"
        ref="videoRef"
        @play="onPlay"
        @pause="onPause"
      />
      <img
        v-if="!videoStatus"
        @click="onPlay"
        :src="pauseImage"
        class="absolute top-[50%] left-[50%] translate-x-[-50%] translate-y-[-50%] z-10"
      />
    </van-barrage>
  </div>
</template>
