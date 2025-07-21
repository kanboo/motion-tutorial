<script setup>
import HeadlineMotion from "./HeadlineMotion.vue";

const headlineString = "Motion 08: Gesture Animations";

const headlineArray = [
  "帶有 Framer Motion 的文本動畫",
  "Text Animations with Framer Motion",
  "這個組件展示了如何使用 Framer Motion 創建文本動畫。",
];
</script>

<template>
  <!-- 單行 -->
  <HeadlineMotion :headline="headlineString" />

  <!-- 多行 -->
  <HeadlineMotion
    :headline="headlineArray"
    class="mt-30"
  />
</template>
