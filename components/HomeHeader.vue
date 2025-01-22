<script setup lang="ts">
import bilibiliImage from '@/assets/images/bilibili.png'
import { ref } from 'vue'
const value = ref('')
</script>

<template>
  <div
    class="h-[40px] flex items-center justify-around fixed top-0 left-0 w-full z-50"
    style="background: linear-gradient(90deg, #eb314d, #501021)"
  >
    <img
      :src="bilibiliImage"
      class="h-[22px]"
    />
    <van-search
      v-model="value"
      placeholder="今年上B站弹幕看春晚"
      shape="round"
      background="transparent"
    />
    <van-image
      width="22px"
      height="22px"
      fit="cover"
      round
      class="border-2 border-white"
      src="http://localhost:3000/video-image/avatar.png"
    />
    <van-button
      type="primary"
      size="mini"
      round
      >立即预约</van-button
    >
  </div>
</template>

<style scoped>
:deep(.van-search) {
  padding: 0;
}

:deep(.van-search__content) {
  background: transparent;
  display: flex;
  align-items: center;
  border: 1px solid #ff8875;
  height: 25px;
  width: 160px;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}

:deep(.van-field__control) {
  font-size: 12px;
  line-height: 16px;
  color: white;
}

:deep(.van-field__control::placeholder) {
  color: #ff8875;
}

:deep(.van-icon-search) {
  font-size: 16px;
  color: #ff8875;
}

:deep(.van-button) {
  background: linear-gradient(0deg, rgba(252, 235, 167, 0.3), rgba(255, 235, 128, 0.3)),
    linear-gradient(0deg, #fd8d4c, #f0e7b3);
  color: #3e040b;
  padding: 12px;
  font-weight: 600;
  font-size: 12px;
}
</style>
