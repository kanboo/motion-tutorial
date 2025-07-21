<script setup>
// Motion 09: whileInView 滾動進場動畫範例
// 展示四大區塊的不同滾動動畫效果
import { motion } from "motion-v";
import HeadlineMotion from "./HeadlineMotion.vue";

// 區塊標題配置
const section1Title = "第一區塊：文字滑入效果";
const section2Title = "第二區塊：卡片彈起效果";
const section3Title = "第三區塊：依序進場效果";
const section4Title = ["第四區塊：複雜動畫組合", "Complex Animation Combination", "結合多種動畫效果的綜合展示"];

// 第三區塊的項目列表
const staggerItems = [
  { id: 1, title: "項目一", desc: "從左側滑入", color: "#ff0088" },
  { id: 2, title: "項目二", desc: "延遲 0.2 秒", color: "#4ff0b7" },
  { id: 3, title: "項目三", desc: "延遲 0.4 秒", color: "#0d63f8" },
  { id: 4, title: "項目四", desc: "延遲 0.6 秒", color: "#f7b801" }
];
</script>

<template>
  <div class="motion-09-container">
    <!-- 第一區塊：文字滑入效果 -->
    <section class="section section-1">
      <motion.div
        :initial="{ x: -100, opacity: 0 }"
        :while-in-view="{ x: 0, opacity: 1 }"
        :transition="{ duration: 0.8, ease: 'easeOut' }"
        :viewport="{ once: true, margin: '-100px' }"
      >
        <h2 class="section-title">{{ section1Title }}</h2>
        <motion.p
          :initial="{ x: -50, opacity: 0 }"
          :while-in-view="{ x: 0, opacity: 1 }"
          :transition="{ duration: 0.6, delay: 0.3 }"
          :viewport="{ once: true }"
          class="section-desc"
        >
          當滾動到此區塊時，標題和描述文字會從左側平滑滑入，並伴隨透明度的變化。
          這是最基本的滾動進場動畫效果。
        </motion.p>
      </motion.div>
    </section>

    <!-- 第二區塊：卡片彈起效果 -->
    <section class="section section-2">
      <motion.div
        :initial="{ y: 100, opacity: 0, scale: 0.8 }"
        :while-in-view="{ y: 0, opacity: 1, scale: 1 }"
        :transition="{ 
          duration: 0.6, 
          type: 'spring', 
          stiffness: 100, 
          damping: 15 
        }"
        :viewport="{ once: true, margin: '-50px' }"
      >
        <h2 class="section-title">{{ section2Title }}</h2>
      </motion.div>
      
      <div class="card-grid">
        <motion.div
          v-for="(item, index) in 3"
          :key="index"
          :initial="{ y: 80, opacity: 0, scale: 0.9 }"
          :while-in-view="{ y: 0, opacity: 1, scale: 1 }"
          :transition="{ 
            duration: 0.5, 
            delay: index * 0.2,
            type: 'spring',
            stiffness: 120
          }"
          :viewport="{ once: true }"
          class="card"
        >
          <div class="card-content">
            <h3>卡片 {{ index + 1 }}</h3>
            <p>這是第 {{ index + 1 }} 張卡片，會依序從下方彈起進場。</p>
          </div>
        </motion.div>
      </div>
    </section>

    <!-- 第三區塊：依序進場效果 -->
    <section class="section section-3">
      <motion.div
        :initial="{ opacity: 0, y: 50 }"
        :while-in-view="{ opacity: 1, y: 0 }"
        :transition="{ duration: 0.6 }"
        :viewport="{ once: true }"
      >
        <h2 class="section-title">{{ section3Title }}</h2>
      </motion.div>

      <div class="stagger-container">
        <motion.div
          v-for="(item, index) in staggerItems"
          :key="item.id"
          :initial="{ x: -60, opacity: 0, rotate: -5 }"
          :while-in-view="{ x: 0, opacity: 1, rotate: 0 }"
          :transition="{ 
            duration: 0.5, 
            delay: index * 0.15,
            ease: 'easeOut'
          }"
          :viewport="{ once: true, margin: '-20px' }"
          class="stagger-item"
          :style="{ borderLeftColor: item.color }"
        >
          <div class="item-indicator" :style="{ backgroundColor: item.color }"></div>
          <div class="item-content">
            <h4>{{ item.title }}</h4>
            <p>{{ item.desc }}</p>
          </div>
        </motion.div>
      </div>
    </section>

    <!-- 第四區塊：複雜動畫組合 -->
    <section class="section section-4">
      <motion.div
        :initial="{ opacity: 0, scale: 0.5, rotate: -10 }"
        :while-in-view="{ opacity: 1, scale: 1, rotate: 0 }"
        :transition="{ 
          duration: 1,
          type: 'spring',
          stiffness: 80,
          damping: 20
        }"
        :viewport="{ once: true, margin: '-100px' }"
        class="complex-animation-wrapper"
      >
        <HeadlineMotion :headline="section4Title" />
      </motion.div>

      <div class="complex-grid">
        <motion.div
          :initial="{ x: -100, rotate: -45, opacity: 0 }"
          :while-in-view="{ x: 0, rotate: 0, opacity: 1 }"
          :transition="{ duration: 0.8, delay: 0.2 }"
          :viewport="{ once: true }"
          class="complex-item item-1"
        >
          <div class="rotating-element"></div>
          <p>旋轉進場</p>
        </motion.div>

        <motion.div
          :initial="{ y: -100, scale: 0, opacity: 0 }"
          :while-in-view="{ y: 0, scale: 1, opacity: 1 }"
          :transition="{ 
            duration: 0.6, 
            delay: 0.4,
            type: 'spring',
            stiffness: 200
          }"
          :viewport="{ once: true }"
          class="complex-item item-2"
        >
          <div class="bouncing-element"></div>
          <p>彈跳進場</p>
        </motion.div>

        <motion.div
          :initial="{ x: 100, y: 100, opacity: 0, filter: 'blur(10px)' }"
          :while-in-view="{ x: 0, y: 0, opacity: 1, filter: 'blur(0px)' }"
          :transition="{ duration: 1, delay: 0.6 }"
          :viewport="{ once: true }"
          class="complex-item item-3"
        >
          <div class="blurring-element"></div>
          <p>模糊清晰化</p>
        </motion.div>
      </div>

      <!-- 最終效果：組合動畫 -->
      <motion.div
        :initial="{ 
          opacity: 0, 
          scale: 0.3, 
          y: 100, 
          rotate: 180,
          filter: 'hue-rotate(180deg)'
        }"
        :while-in-view="{ 
          opacity: 1, 
          scale: 1, 
          y: 0, 
          rotate: 0,
          filter: 'hue-rotate(0deg)'
        }"
        :transition="{ 
          duration: 1.5, 
          delay: 0.8,
          type: 'spring',
          stiffness: 60
        }"
        :viewport="{ once: true }"
        class="final-showcase"
      >
        <div class="showcase-content">
          <h3>🎉 終極展示</h3>
          <p>結合縮放、旋轉、位移、濾鏡等多種效果的複合動畫</p>
        </div>
      </motion.div>
    </section>
  </div>
</template>

<style scoped>
.motion-09-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 2rem;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
}

.section {
  min-height: 100vh;
  padding: 4rem 0;
  margin-bottom: 2rem;
}

.section-title {
  font-size: 2.5rem;
  font-weight: 700;
  margin-bottom: 1.5rem;
  color: #1a1a1a;
  text-align: center;
}

.section-desc {
  font-size: 1.1rem;
  line-height: 1.6;
  color: #666;
  max-width: 600px;
  margin: 0 auto;
  text-align: center;
}

/* 第一區塊樣式 */
.section-1 {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  border-radius: 20px;
  padding: 4rem 2rem;
}

.section-1 .section-title,
.section-1 .section-desc {
  color: white;
}

/* 第二區塊樣式 */
.section-2 {
  background: #f8fafc;
  border-radius: 20px;
  padding: 4rem 2rem;
}

.card-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 2rem;
  margin-top: 3rem;
}

.card {
  background: white;
  border-radius: 16px;
  padding: 2rem;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
  border: 1px solid #e2e8f0;
  transition: transform 0.2s ease;
}

.card:hover {
  transform: translateY(-5px);
}

.card-content h3 {
  font-size: 1.5rem;
  font-weight: 600;
  margin-bottom: 1rem;
  color: #2d3748;
}

.card-content p {
  color: #718096;
  line-height: 1.5;
}

/* 第三區塊樣式 */
.section-3 {
  background: linear-gradient(135deg, #ff9a9e 0%, #fecfef 100%);
  border-radius: 20px;
  padding: 4rem 2rem;
}

.stagger-container {
  margin-top: 3rem;
  max-width: 600px;
  margin-left: auto;
  margin-right: auto;
}

.stagger-item {
  background: white;
  border-radius: 12px;
  padding: 1.5rem;
  margin-bottom: 1rem;
  display: flex;
  align-items: center;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
  border-left: 4px solid #ff0088;
}

.item-indicator {
  width: 12px;
  height: 12px;
  border-radius: 50%;
  margin-right: 1rem;
  flex-shrink: 0;
}

.item-content h4 {
  font-size: 1.2rem;
  font-weight: 600;
  margin-bottom: 0.5rem;
  color: #2d3748;
}

.item-content p {
  color: #718096;
  margin: 0;
}

/* 第四區塊樣式 */
.section-4 {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  border-radius: 20px;
  padding: 4rem 2rem;
  color: white;
}

.complex-animation-wrapper {
  text-align: center;
  margin-bottom: 4rem;
}

.complex-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 2rem;
  margin-bottom: 4rem;
}

.complex-item {
  background: rgba(255, 255, 255, 0.1);
  border-radius: 16px;
  padding: 2rem;
  text-align: center;
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.2);
}

.rotating-element,
.bouncing-element,
.blurring-element {
  width: 60px;
  height: 60px;
  margin: 0 auto 1rem;
  border-radius: 50%;
}

.rotating-element {
  background: linear-gradient(45deg, #ff0088, #4ff0b7);
}

.bouncing-element {
  background: linear-gradient(45deg, #4ff0b7, #0d63f8);
}

.blurring-element {
  background: linear-gradient(45deg, #0d63f8, #f7b801);
}

.complex-item p {
  color: white;
  font-weight: 500;
}

.final-showcase {
  background: rgba(255, 255, 255, 0.15);
  border-radius: 20px;
  padding: 3rem;
  text-align: center;
  backdrop-filter: blur(15px);
  border: 2px solid rgba(255, 255, 255, 0.3);
}

.showcase-content h3 {
  font-size: 2rem;
  margin-bottom: 1rem;
  color: white;
}

.showcase-content p {
  font-size: 1.1rem;
  color: rgba(255, 255, 255, 0.9);
  max-width: 500px;
  margin: 0 auto;
}

/* 響應式設計 */
@media (max-width: 768px) {
  .motion-09-container {
    padding: 1rem;
  }
  
  .section {
    padding: 2rem 0;
  }
  
  .section-title {
    font-size: 2rem;
  }
  
  .card-grid {
    grid-template-columns: 1fr;
  }
  
  .complex-grid {
    grid-template-columns: 1fr;
  }
}
</style>