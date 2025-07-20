<script setup>
// AnimatePresence 允許你為那些從 DOM 中移除的元件添加退場動畫。
// 通常情況下，當元件被卸載時，它們會立即從 DOM 中消失，無法執行動畫。AnimatePresence 解決了這個問題。
// ref: https://motion.dev/docs/vue-animate-presence

import AnimatePresenceSync from './AnimatePresenceSync.vue';
import AnimatePresenceWait from './AnimatePresenceWait.vue';
import AnimatePresencePopLayout from './AnimatePresencePopLayout.vue';
</script>

<template>
  <div class="container">
    <!-- mode="sync"：進場與退場動畫同時執行（預設）。 -->
    <AnimatePresenceSync />

    <!-- mode="wait"：等待退場動畫完成後才執行進場動畫。 -->
    <AnimatePresenceWait />

    <!-- mode="popLayout"：進場動畫會在退場動畫結束後執行，且 layout 會 pop。 -->
    <AnimatePresencePopLayout />
  </div>
</template>

<style>
.container {
  display: flex;
  flex-direction: column;
  gap: 32px;
  width: 320px;
  min-height: 600px;
  position: relative;
}
.box {
  width: 100px;
  height: 60px;
  background-color: #0cdcf7;
  border-radius: 10px;
  margin-bottom: 8px;
  transition: box-shadow 0.2s;
  box-shadow: 0 2px 8px rgba(0,0,0,0.08);
}
.btn-row {
  display: flex;
  gap: 8px;
  margin-bottom: 12px;
}
.action {
  background-color: #f7b801;
  border-radius: 6px;
  padding: 6px 16px;
  color: #0f1115;
  border: none;
  cursor: pointer;
  font-size: 1rem;
}
.action:disabled {
  background-color: #e0e0e0;
  color: #b0b0b0;
  cursor: not-allowed;
  opacity: 0.7;
}
h2 {
  font-size: 1rem;
  margin: 0 0 8px 0;
  color: #0f1115;
}
</style>
