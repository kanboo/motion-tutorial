<script setup>
import { ref } from 'vue';
import { AnimatePresence, motion } from 'motion-v';
const boxesPop = ref([1, 2, 3]);
let nextIdPop = 4;
function addBoxPop() {
  boxesPop.value.push(nextIdPop++);
}
function removeBoxPop() {
  boxesPop.value.pop();
}
</script>
<template>
  <div>
    <h2>AnimatePresencePopLayout（mode="popLayout"）</h2>
    <div class="btn-row">
      <button
        class="action"
        @click="addBoxPop"
      >
        新增
      </button>
      <button
        class="action"
        @click="removeBoxPop"
      >
        移除
      </button>
    </div>
    <AnimatePresence
      :initial="false"
      mode="popLayout"
    >
      <motion.div
        v-for="id in boxesPop"
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
