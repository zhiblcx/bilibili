<script setup lang="ts">
defineProps({
  videoImage: {
    type: String,
    required: true
  },
  playCount: {
    type: String,
    required: true
  },
  commentCount: {
    type: String,
    required: true
  },
  description: {
    type: String,
    required: true
  }
})
</script>

<template>
  <div class="w-[46%]">
    <div class="relative">
      <div
        class="absolute z-40 bottom-2 right-0 w-[100%] h-[30px]"
        style="background: linear-gradient(0deg, rgba(0, 0, 0, 0.85), transparent)"
      ></div>

      <div class="text-white absolute left-2 bottom-[13px] z-40 flex">
        <van-icon
          name="play-circle-o"
          class="mr-1"
        />
        <span class="text-xs">{{ playCount }}</span>
      </div>

      <div class="text-white absolute right-2 bottom-[13px] z-40 flex">
        <van-icon
          name="comment-circle-o"
          class="mr-1"
        />
        <span class="text-xs">{{ commentCount }}</span>
      </div>

      <van-image
        width="100%"
        height="100"
        fit="contain"
        :src="videoImage"
        class="shadow-sm"
      />
    </div>

    <span class="text-xs line-clamp-2">{{ description }}</span>
  </div>
</template>
