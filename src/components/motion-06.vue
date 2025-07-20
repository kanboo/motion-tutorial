<script setup>
// ref: https://motion.dev/docs/vue-animation#keyframes
import { motion } from "motion-v";
</script>

<template>
  <motion.div
    class="box"
    :while-hover="{
      scale: [null, 1.1, 1.6],
      transition: {
        duration: 0.5,
        times: [0, 0.6, 1],
        ease: ['easeInOut', 'easeOut']
      }
    }"
    :transition="{
      duration: 0.3,
      ease: 'easeOut'
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
