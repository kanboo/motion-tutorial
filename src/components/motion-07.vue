<script setup>
// ref: https://motion.dev/docs/vue-animation#gesture-animations
import { motion } from "motion-v";
import { ElButton } from "element-plus";
</script>

<template>
  <motion.div
    :while-hover="{ scale: 1.2 }"
    :while-press="{ scale: 0.8 }"
    class="box"
  />
  <motion.div
    :while-press="{ scale: 0.8 }"
    style="margin-top: 20px; display: inline-block;"
  >
    <el-button type="primary">
      Motion Button
    </el-button>
  </motion.div>
</template>


<style>
  .box {
    width: 100px;
    height: 100px;
    background-color: #0d63f8;
    border-radius: 10px;
  }
</style>
