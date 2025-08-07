<script setup>
import { ref, onMounted } from 'vue';
import { motion } from 'motion-v';
import gachaImage from '../assets/gacha-default-image.png';

// 星星資料
const stars = ref([]);
const container = ref(null);

// 產生隨機數字的工具函式
const random = (min, max) => Math.random() * (max - min) + min;

// 產生隨機星星 - 在圖片周邊30px環繞
const generateStar = (id) => {
  const centerX = 50; // 中心點X (%)
  const centerY = 50; // 中心點Y (%)

  // 圖片尺寸：120px寬，9:16比例
  const imageWidth = 120;
  const imageHeight = imageWidth * (16/9); // 約213px

  // 容器尺寸
  const containerWidth = 800; // 估計值，可根據實際調整
  const containerHeight = 400;

  // 轉換為百分比
  const imageWidthPercent = (imageWidth / containerWidth) * 100; // 約15%
  const imageHeightPercent = (imageHeight / containerHeight) * 100; // 約53%

  // 30px環繞區域
  const ringSize = 30;
  const ringWidthPercent = (ringSize / containerWidth) * 100; // 約3.75%
  const ringHeightPercent = (ringSize / containerHeight) * 100; // 約7.5%

  // 隨機選擇生成模式：40%環繞，30%圖片上方，30%其他區域
  const mode = Math.random();
  const shouldRing = mode < 0.4;
  const shouldOverImage = mode >= 0.4 && mode < 0.7;

  let x, y;

  if (shouldRing) {
    // 環繞模式：在圖片周圍30px範圍內生成
    const angle = random(0, Math.PI * 2);

    // 橢圓環形的內外半徑
    const innerRadiusX = imageWidthPercent / 2;
    const outerRadiusX = imageWidthPercent / 2 + ringWidthPercent;
    const innerRadiusY = imageHeightPercent / 2;
    const outerRadiusY = imageHeightPercent / 2 + ringHeightPercent;

    // 在內外環之間隨機選擇距離
    const radiusX = random(innerRadiusX, outerRadiusX);
    const radiusY = random(innerRadiusY, outerRadiusY);

    // 計算環繞位置
    x = centerX + radiusX * Math.cos(angle);
    y = centerY + radiusY * Math.sin(angle);

    // 確保在容器範圍內
    x = Math.max(3, Math.min(97, x));
    y = Math.max(3, Math.min(97, y));
  } else if (shouldOverImage) {
    // 圖片上方模式：在圖片範圍內生成
    x = random(centerX - imageWidthPercent/3, centerX + imageWidthPercent/3);
    y = random(centerY - imageHeightPercent/3, centerY + imageHeightPercent/3);

    // 確保在容器範圍內
    x = Math.max(3, Math.min(97, x));
    y = Math.max(3, Math.min(97, y));
  } else {
    // 其他區域模式：避開圖片和環繞區域
    let attempts = 0;
    do {
      x = random(3, 97);
      y = random(3, 97);
      attempts++;
    } while (
      attempts < 50 &&
      x > centerX - (imageWidthPercent/2 + ringWidthPercent) &&
      x < centerX + (imageWidthPercent/2 + ringWidthPercent) &&
      y > centerY - (imageHeightPercent/2 + ringHeightPercent) &&
      y < centerY + (imageHeightPercent/2 + ringHeightPercent)
    );
  }

  return {
    id,
    x,
    y,
    size: random(6, 18),
    opacity: random(0.4, 1),
    animationDelay: random(0, 3),
    duration: random(2, 4),
    // 所有星星都使用白色系列，根據位置調整亮度
    color: shouldRing ?
      ['#FFFFFF', '#F8F8FF', '#FFE4E1'][Math.floor(Math.random() * 3)] : // 環繞星星更亮
      shouldOverImage ?
      ['#FFFFFF', '#F8F8FF', '#E6E6FA'][Math.floor(Math.random() * 3)] : // 圖片上方星星亮白色
      ['#F5F5F5', '#E6E6FA', '#F0F8FF'][Math.floor(Math.random() * 3)],  // 其他星星稍暗
    isOverImage: shouldOverImage
  };
};

// 初始化星星
const initStars = () => {
  const starCount = 40; // 增加星星數量以填滿環繞區域
  stars.value = Array.from({ length: starCount }, (_, i) => generateStar(i));
};

// 閃爍動畫變體
const twinkleVariants = {
  hidden: {
    opacity: 0,
    scale: 0.5
  },
  visible: (star) => ({
    opacity: [0.3, 1, 0.3],
    scale: [0.5, 1.2, 0.8, 1],
    transition: {
      duration: star.duration,
      repeat: Infinity,
      delay: star.animationDelay,
      ease: "easeInOut"
    }
  })
};

// 浮動動畫變體
const floatVariants = {
  animate: (star) => ({
    y: [0, -10, 0],
    x: [0, random(-5, 5), 0],
    transition: {
      duration: random(5, 8),
      repeat: Infinity,
      ease: "easeInOut",
      delay: random(0, 3)
    }
  })
};

// 新增星星按鈕處理
const addRandomStars = () => {
  const newStars = Array.from({ length: 8 }, (_, i) =>
    generateStar(stars.value.length + i)
  );
  stars.value.push(...newStars);
};

// 清除所有星星
const clearStars = () => {
  stars.value = [];
};

// 重置星星
const resetStars = () => {
  clearStars();
  setTimeout(() => {
    initStars();
  }, 500);
};

onMounted(() => {
  initStars();
});
</script>

<template>
  <div class="star-demo">
    <h2 class="demo-title">
      ✨ 星星特效展示
    </h2>

    <div class="controls">
      <button
        class="btn btn-primary"
        @click="addRandomStars"
      >
        ➕ 新增星星
      </button>
      <button
        class="btn btn-secondary"
        @click="resetStars"
      >
        🔄 重置
      </button>
      <button
        class="btn btn-danger"
        @click="clearStars"
      >
        🗑️ 清除
      </button>
      <div class="star-count">
        星星數量: {{ stars.length }}
      </div>
    </div>

    <div
      ref="container"
      class="star-container"
    >
      <!-- 背景漸變 -->
      <div class="background" />

      <!-- 中央圖片 -->
      <div class="center-image">
        <img
          :src="gachaImage"
          alt="Gacha Default Image"
          class="gacha-image"
        >
      </div>

      <!-- 星星們 -->
      <motion.div
        v-for="star in stars"
        :key="star.id"
        :variants="twinkleVariants"
        :custom="star"
        initial="hidden"
        animate="visible"
        :style="{
          position: 'absolute',
          left: `${star.x}%`,
          top: `${star.y}%`,
          width: `${star.size}px`,
          height: `${star.size}px`,
          transformOrigin: 'center',
          zIndex: star.isOverImage ? 20 : 10,
        }"
        class="star"
      >
        <svg
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 784.11 815.53"
          :style="{ fill: star.color }"
          class="star-svg"
        >
          <path d="M392.05 0c-20.9,210.08 -184.06,378.41 -392.05,407.78 207.96,29.37 371.12,197.68 392.05,407.74 20.93,-210.06 184.09,-378.37 392.05,-407.74 -207.98,-29.38 -371.16,-197.69 -392.06,-407.78z" />
        </svg>
      </motion.div>

      <!-- 額外的浮動效果星星 -->
      <motion.div
        v-for="star in stars.slice(0, 10)"
        :key="`float-${star.id}`"
        :variants="floatVariants"
        :custom="star"
        animate="animate"
        :style="{
          position: 'absolute',
          left: `${star.x + 5}%`,
          top: `${star.y + 5}%`,
          width: `${star.size * 0.7}px`,
          height: `${star.size * 0.7}px`,
          opacity: 0.6,
        }"
        class="floating-star"
      >
        <svg
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 784.11 815.53"
          :style="{ fill: star.color }"
          class="star-svg floating-star-svg"
        >
          <path d="M392.05 0c-20.9,210.08 -184.06,378.41 -392.05,407.78 207.96,29.37 371.12,197.68 392.05,407.74 20.93,-210.06 184.09,-378.37 392.05,-407.74 -207.98,-29.38 -371.16,-197.69 -392.06,-407.78z" />
        </svg>
      </motion.div>
    </div>

    <div class="info">
      <p>
        🌟 此範例展示了：
      </p>
      <ul>
        <li>隨機生成星星位置、大小和顏色</li>
        <li>中央圖片採用 9:16 長寬比顯示</li>
        <li>星星圍繞圖片周圍生成，避免重疊</li>
        <li>星星可以顯示在圖片上方（亮白色星星）</li>
        <li>使用 motion-v 的 variants 建立複雜動畫</li>
        <li>閃爍效果（透明度、縮放、旋轉）</li>
        <li>浮動動畫效果</li>
        <li>無限循環動畫與隨機延遲</li>
        <li>動態新增與移除星星</li>
      </ul>
    </div>
  </div>
</template>

<style scoped>
.star-demo {
  padding: 20px;
  min-height: 100vh;
  background: #000000;
  color: white;
  overflow: hidden;
}

.demo-title {
  text-align: center;
  margin-bottom: 20px;
  font-size: 2rem;
  background: linear-gradient(45deg, #FFFFFF, #F8F8FF, #E6E6FA);
  background-clip: text;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  animation: titleGlow 3s ease-in-out infinite alternate;
}

@keyframes titleGlow {
  from { text-shadow: 0 0 10px rgba(255, 255, 255, 0.5); }
  to { text-shadow: 0 0 20px rgba(255, 255, 255, 0.8), 0 0 30px rgba(255, 255, 255, 0.6); }
}

.controls {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 15px;
  margin-bottom: 20px;
  flex-wrap: wrap;
}

.btn {
  padding: 10px 20px;
  border: none;
  border-radius: 25px;
  cursor: pointer;
  font-weight: bold;
  transition: all 0.3s ease;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
}

.btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(0, 0, 0, 0.3);
}

.btn-primary {
  background: linear-gradient(45deg, #667eea 0%, #764ba2 100%);
  color: white;
}

.btn-secondary {
  background: linear-gradient(45deg, #f093fb 0%, #f5576c 100%);
  color: white;
}

.btn-danger {
  background: linear-gradient(45deg, #ff6b6b 0%, #ee5a24 100%);
  color: white;
}

.star-count {
  background: rgba(255, 255, 255, 0.1);
  padding: 8px 15px;
  border-radius: 20px;
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.2);
}

.star-container {
  position: relative;
  height: 400px;
  border-radius: 20px;
  overflow: hidden;
  margin-bottom: 30px;
  border: 2px solid rgba(255, 255, 255, 0.1);
  box-shadow:
    inset 0 0 50px rgba(255, 255, 255, 0.05),
    0 10px 40px rgba(0, 0, 0, 0.3);
}

.background {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: #000000;
}

.center-image {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 15;
  width: 120px;
  aspect-ratio: 9 / 16;
  border-radius: 12px;
  overflow: hidden;
  box-shadow:
    0 0 30px rgba(255, 255, 255, 0.3),
    0 0 60px rgba(255, 255, 255, 0.1),
    inset 0 0 20px rgba(255, 255, 255, 0.1);
  border: 2px solid rgba(255, 255, 255, 0.2);
}

.gacha-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
}

.star {
  cursor: pointer;
  user-select: none;
  filter: drop-shadow(0 0 6px currentColor);
}

.star-svg {
  width: 100%;
  height: 100%;
  filter: drop-shadow(0 0 8px currentColor);
  transition: filter 0.3s ease;
}

.floating-star {
  user-select: none;
  pointer-events: none;
  z-index: 5;
}

.floating-star-svg {
  width: 100%;
  height: 100%;
  filter: drop-shadow(0 0 4px currentColor);
}

.star:hover .star-svg {
  filter: drop-shadow(0 0 16px currentColor) drop-shadow(0 0 32px currentColor);
}

.info {
  background: rgba(255, 255, 255, 0.05);
  border-radius: 15px;
  padding: 20px;
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.1);
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.2);
}

.info h3 {
  margin-top: 0;
  color: #FFD700;
}

.info ul {
  margin-left: 20px;
}

.info li {
  margin-bottom: 8px;
  line-height: 1.6;
}

.info p {
  margin-bottom: 15px;
  font-weight: bold;
  font-size: 1.1rem;
}

/* 響應式設計 */
@media (max-width: 768px) {
  .star-demo {
    padding: 15px;
  }

  .demo-title {
    font-size: 1.5rem;
  }

  .controls {
    flex-direction: column;
    gap: 10px;
  }

  .btn {
    padding: 8px 16px;
    font-size: 14px;
  }

  .star-container {
    height: 300px;
  }

  .info {
    padding: 15px;
  }
}
</style>
