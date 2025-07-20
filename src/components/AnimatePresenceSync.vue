<script setup>
import { ref } from 'vue';
import { AnimatePresence, motion } from 'motion-v';
const boxesSync = ref([1, 2, 3]);
let nextIdSync = 4;
function addBoxSync() {
  boxesSync.value.push(nextIdSync++);
}
function removeBoxSync() {
  boxesSync.value.pop();
}
</script>
<template>
  <div>
    <h2>AnimatePresenceSync（mode="sync"）</h2>
    <div class="btn-row">
      <button
        class="action"
        @click="addBoxSync"
      >
        新增
      </button>
      <button
        class="action"
        @click="removeBoxSync"
      >
        移除
      </button>
    </div>
    <AnimatePresence
      :initial="false"
      mode="sync"
    >
      <motion.div
        v-for="id in boxesSync"
        :key="id"
        :initial="{ opacity: 0, x: -100, scale: 0.5, backgroundColor: '#f7b801' }"
        :animate="{ opacity: 1, x: 0, scale: 1, backgroundColor: '#0cdcf7' }"
        :exit="{ opacity: 0, x: 100, scale: 0.5, backgroundColor: '#f7b801' }"
        :transition="{ duration: 0.8 }"
        class="box"
      />
    </AnimatePresence>
  </div>
</template>
