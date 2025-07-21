<script setup>
import { motion } from "motion-v";
import { computed } from "vue";

// 接收 props: headline (可以是單行字串或多行陣列)
const props = defineProps({
  headline: {
    type: [String, Array],
    required: true
  }
});

// headlineLines: 每行物件，包含字元陣列與動畫起始延遲
const headlineLines = computed(() => {
  // headline 可能是 string 或 array，統一轉成 array 處理
  const lines = Array.isArray(props.headline) ? props.headline : [props.headline];
  return lines.map((line, i, arr) => {
    // 計算本行動畫起始延遲（前面所有行的字元總延遲）
    const startDelay = arr.slice(0, i).reduce((acc, l) => acc + l.length * 0.1, 0);
    // console.log(`Processing line ${i + 1}: "${line}"`);
    // console.log(`Line ${i} start delay: ${startDelay}`);
    return {
      letters: line.split(""), // 將本行拆成字元陣列
      startDelay
    };
  });
});
</script>

<template>
  <div>
    <!-- 逐行渲染 headline，每行分別動畫 -->
    <div
      v-for="(line, lineIndex) in headlineLines"
      :key="lineIndex"
      class="mb-2"
    >
      <!-- 逐字渲染，每個字元獨立動畫，延遲依行與字元序號計算 -->
      <motion.span
        v-for="(letter, index) in line.letters"
        :key="`${lineIndex}-${index}`"
        :initial="{ filter: 'blur(10px)', opacity: 0, y: 12 }"
        :animate="{ filter: 'blur(0)', opacity: 1, y: 0 }"
        :transition="{ delay: line.startDelay + index * 0.1, duration: 0.5 }"
        class="text-2xl font-bold inline-block"
      >
        <!-- 空白字元以不換行空格顯示 -->
        {{ letter === ' ' ? '\u00A0' : letter }}
      </motion.span>
    </div>
  </div>
</template>
