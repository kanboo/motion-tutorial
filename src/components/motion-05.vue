<script setup>
// ref: https://motion.dev/docs/vue-animation#keyframes
import { motion } from "motion-v"
</script>

<template>
    <motion.div
        :animate="{
            scale: [1, 2, 2, 1, 1],
            rotate: [0, 0, 180, 180, 0],
            borderRadius: ['0%', '0%', '50%', '50%', '0%']
        }"
        :transition="{
            // duration 是動畫持續時間，單位為「秒」(s)。
            // 例如 duration: 4 代表動畫會執行 4 秒。
            duration: 4,
            ease: 'easeInOut',
            // times 是一個陣列，代表每個 keyframe 在整個動畫中的相對時間點，單位是「百分比」(0~1 之間的小數)。
            // 例如 times: [0, 0.2, 0.5, 0.8, 1]，0 代表動畫開始，1 代表動畫結束。
            times: [0, 0.2, 0.5, 0.8, 1],
            repeat: Infinity,
            repeatDelay: 1
        }"
        class="box"
    />
</template>

<style>
.box {
    width: 100px;
    height: 100px;
    background-color: #f5f5f5;
    border-radius: 5px;
}
</style>
