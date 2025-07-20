<script setup>
import { ref } from 'vue';
import { AnimatePresence, motion } from 'motion-v';
import AnimatePresenceWaitViewA from './AnimatePresenceWaitViewA.vue';
import AnimatePresenceWaitViewB from './AnimatePresenceWaitViewB.vue';
const currentView = ref('A');
function toggleView() {
  currentView.value = currentView.value === 'A' ? 'B' : 'A';
}
</script>
<template>
  <div>
    <h2>AnimatePresenceWait（mode="wait"）</h2>
    <div class="btn-row">
      <button
        class="action"
        @click="toggleView"
      >
        切換元件（目前：{{ currentView }})
      </button>
    </div>
    <AnimatePresence mode="wait">
      <motion.div
        :key="currentView"
        :initial="{ opacity: 0, x: -100, scale: 0.5 }"
        :animate="{ opacity: 1, x: 0, scale: 1 }"
        :exit="{ opacity: 0, x: 100, scale: 0.5 }"
        :transition="{ duration: 0.8 }"
        class="box"
      >
        <component :is="currentView === 'A' ? AnimatePresenceWaitViewA : AnimatePresenceWaitViewB" />
      </motion.div>
    </AnimatePresence>
  </div>
</template>
