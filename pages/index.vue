<script setup lang="ts">
import { ref } from 'vue'
import { useFetch, useRouter } from '#app'
import type { HomeType } from '~/types/home'
const { data: homeData } = await useFetch('/api/home')
const active = ref(0)
const loading = ref(false)
const finished = ref(false)
const page = ref(1)
const pageSize = ref(10)
const router = useRouter()
const cardData = ref<HomeType | []>(
  homeData?.value?.data[active.value]?.data.slice((page.value - 1) * pageSize.value, page.value * pageSize.value) || []
)

const onClickTab = () => {
  page.value = 1
  pageSize.value = 10
  finished.value = false
  cardData.value =
    homeData?.value?.data[active.value].data?.slice((page.value - 1) * pageSize.value, page.value * pageSize.value) ||
    []
}

const onLoad = () => {
  setTimeout(() => {
    loading.value = true
    if (cardData?.value?.length === homeData?.value?.data[active.value].data.length) {
      finished.value = true
    } else {
      page.value++
      const data =
        homeData?.value?.data[active.value].data.slice(
          (page.value - 1) * pageSize.value,
          page.value * pageSize.value
        ) || []
      cardData.value = [...cardData.value, ...data]
    }
    loading.value = false
  }, 500)
}
</script>

<template>
  <NuxtLayout name="home-layouts" />
  <van-tabs
    v-model:active="active"
    @click-tab="onClickTab"
    offset-top="40px"
    sticky
    class="mt-[42px]"
  >
    <van-tab
      :title="data.tab"
      v-for="(data, index) in homeData?.data || []"
      v-bind:key="index"
    />
  </van-tabs>
  <van-list
    v-model:loading="loading"
    :finished="finished"
    finished-text="没有更多了"
    @load="onLoad"
  >
    <div class="flex justify-around flex-wrap">
      <VCard
        v-for="(video, index) in cardData"
        :key="index"
        :play-count="video.playCount"
        :comment-count="video.commentCount"
        :description="video.description"
        :video-image="video.videoImage"
        class="mb-4"
        @click="
          () => {
            router.push('/video/' + index)
          }
        "
      />
    </div>
  </van-list>
</template>

<style>
:root {
  --van-primary-color: #fb86a7;
  --van-tab-active-text-color: var(--van-primary-color);
}
</style>
