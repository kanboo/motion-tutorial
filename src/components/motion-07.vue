<script setup>
// ref: https://motion.dev/docs/vue-animation#gesture-animations
// ref: https://motion.dev/docs/vue-gestures
import { motion } from "motion-v";
import { ElButton } from "element-plus";

// Framer Motion 提供了多種手勢（Gestures）API，讓開發者能夠輕鬆處理用戶交互。以下是主要的手勢類型及其比較：
// 主要手勢類型
// ### 1. **Hover**
// - **觸發條件**：指針懸停在組件上或離開組件
// - **事件**：`@hoverStart`, `@hoverEnd`
// - **動畫屬性**：`whileHover`
// - **特點**：與 onMouseEnter 和 onMouseLeave 不同，hover 保證只會因為實際的滑鼠事件觸發
// - **Mobile**：❌ 在觸控設備上無效

// ### 2. **Press**
// - **觸發條件**：主要指針（如左鍵點擊或第一個觸控點）按下並在同一組件上釋放
// - **事件**：`@press`, `@pressStart`, `@pressCancel`
// - **動畫屬性**：`whilePress`
// - **無障礙支援**：支援鍵盤訪問，可使用 Enter 鍵觸發
// - **Mobile**：✅ 完美支援觸控操作

// ### 3. **Drag**
// - **觸發條件**：將指針移動應用到組件的 x 和/或 y 軸
// - **配置**：`drag`, `drag="x"`, `drag="y"`
// - **動畫屬性**：`whileDrag`
// - **功能**：支援 `dragConstraints`、`dragElastic`、`dragDirectionLock`
// - **Mobile**：✅ 良好支援

// ### 4. **InView**
// - **觸發條件**：元素進入或離開視窗
// - **動畫屬性**：`whileInView`
// - **用途**：滾動動畫、進場效果
// - **Mobile**：✅ 完全支援

// ### 5. **Focus**
// - **觸發條件**：組件獲得或失去焦點（遵循 CSS :focus-visible 規則）
// - **動畫屬性**：`whileFocus`
// - **適用場景**：表單輸入、鍵盤導航
// - **Mobile**：⚠️ 觸控設備焦點行為有限

// ## 使用時機比較表

// | 手勢類型  | 桌面端  | 移動端  | 主要用途          | 性能 |
// |----------|--------|--------|-----------------|------|
// | Hover    | ✅ 主要 | ❌ 無效 | 懸停反饋、預覽     | 輕量 |
// | Press    | ✅ 支援 | ✅ 主要 | 點擊操作、確認     | 輕量 |
// | Drag     | ✅ 精確 | ✅ 良好 | 位置移動、排序     | 中等 |
// | InView   | ✅ 支援 | ✅ 支援 | 滾動動畫、進場效果  | 輕量 |
// | Focus    | ✅ 重要 | ⚠️ 有限 | 鍵盤導航、無障礙    | 輕量 |

</script>

<template>
  <div style="margin-bottom: 8px; color: #000; font-size: 15px;">
    第一個 motion.div：展示 Hover 與 Press 手勢動畫效果的方塊
  </div>
  <!-- 第一個 motion.div：展示 Hover 與 Press 手勢動畫效果的方塊 -->
  <motion.div
    :while-hover="{ scale: 1.2 }"
    :while-press="{ scale: 0.8 }"
    class="box"
    style="margin: auto;"
  />
  <div style="margin-top: 32px;margin-bottom: 8px; color: #000; font-size: 15px;">
    第二個 motion.div：包裹 el-button，展示 Press 手勢動畫效果的按鈕
  </div>
  <!-- 第二個 motion.div：包裹 el-button，展示 Press 手勢動畫效果的按鈕 -->
  <motion.div
    :while-hover="{ scale: 1.2 }"
    :while-press="{ scale: 0.8 }"
    style="margin-top: 20px; margin-bottom: 32px; display: inline-block;"
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
