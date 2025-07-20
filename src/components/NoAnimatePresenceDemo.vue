<script setup>
import { ref } from 'vue';
import { motion } from 'motion-v';

const show = ref(true);
</script>

<template>
  <div>
    <h2>未使用 AnimatePresence：元件消失時無退場動畫</h2>
    <div class="btn-row">
      <button
        class="action"
        @click="show = !show"
      >
        {{ show ? '隱藏' : '顯示' }} Box
      </button>
    </div>
    <motion.div
      v-if="show"
      class="box"
      :initial="{ opacity: 0, y: 30 }"
      :animate="{ opacity: 1, y: 0 }"
      :exit="{ opacity: 0, y: -30 }"
    >
      Box
    </motion.div>
  </div>
</template>

<style scoped>
.box {
  width: 100px;
  height: 60px;
  background-color: #0cdcf7;
  border-radius: 10px;
  margin-bottom: 8px;
  transition: box-shadow 0.2s;
  box-shadow: 0 2px 8px rgba(0,0,0,0.08);
  display: flex;
  align-items: center;
  justify-content: center;
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
