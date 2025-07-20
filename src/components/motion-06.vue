<script setup>
// ref: https://motion.dev/docs/vue-animation#keyframes
import { motion } from "motion-v";

// 請問下列二個寫法有何差異？
// <motion.div :animate="{ x: [0, 100, 0] }" />
// <motion.div :animate="{ x: [null, 100, 0] }" />

// 答：
// 這兩個寫法的差異在於動畫的起始行為：
// 第一種寫法：{ x: [0, 100, 0] }

// 明確指定起始位置為 x: 0
// 無論元素目前的實際位置在哪裡，動畫都會強制從 x: 0 開始
// 如果元素原本就在 x: 50 的位置，它會瞬間跳到 x: 0，然後開始動畫

// 第二種寫法：{ x: [null, 100, 0] }

// null 表示使用元素的當前位置作為起始點
// 動畫會從元素目前所在的位置平滑開始
// 如果元素原本在 x: 50 的位置，動畫會從 50 → 100 → 0

// 簡單來說：
// 第一種會有「跳躍」到起始位置的效果
// 第二種會從當前位置「平滑」開始動畫
// 這在實際應用中很重要，特別是當你的元素可能因為用戶互動或其他動畫而處於不同位置時，使用 null 可以避免不自然的跳躍效果。
</script>

<template>
  <div class="mb-4 text-gray-700 text-sm">
    範例一：scale: [null, 1.5, 1.4]<br>
    會從目前大小平滑開始動畫，避免跳躍。
  </div>
  <motion.div
    class="box"
    :while-hover="{
      scale: [null, 1.5, 1.4],
      transition: {
        duration: 0.3,
        ease: ['easeInOut']
      }
    }"
  />

  <div class="mt-16 mb-4 text-gray-700 text-sm">
    範例二：scale: [0, 1.5, 1.4]<br>
    會強制從 scale 0 開始，可能導致跳躍。
  </div>
  <motion.div
    class="box"
    :while-hover="{
      scale: [0, 1.5, 1.4],
      transition: {
        duration: 0.3,
        ease: ['easeInOut']
      }
    }"
  />
</template>

<style>
.box {
  width: 100px;
  height: 100px;
  background-color: #0cdcf7;
  border-radius: 5px;
}
</style>
