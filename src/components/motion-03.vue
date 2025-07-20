<script setup>
// ref: https://motion.dev/docs/vue-animation#enter-animations
import { motion } from 'motion-v'
</script>

<template>
  <motion.div
    :initial="{ opacity: 0, scale: 0 }"
    :animate="{ opacity: 1, scale: 1 }"
    :transition="{
      duration: 0.4,
      scale: { type: 'spring', visualDuration: 0.8, bounce: 0.6 }
    }"
    class="ball" />
</template>

<style>
.ball {
  width: 100px;
  height: 100px;
  background-color: #8df0cc;
  border-radius: 50%;
}
</style>
