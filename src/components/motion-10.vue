<script setup>
// Motion 10: staggerChildren 錯開子元素動畫範例
// 展示如何使用 staggerChildren 讓多個子元素依序播放動畫

// FIXME: 目前 hover 狀態無法正常工作！

// NOTE:
// 當你在 Framer Motion 中使用 variants 時，
// 直接在元件上設定 whileHover 確實會無效，因為 variants 會覆蓋掉直接設定的動畫屬性。
// 正確的做法是在 variants 物件中定義 hover 狀態：

// const variants = {
//   initial: { scale: 1 },
//   hover: { scale: 1.1 }, // 在 variants 中定義 hover 狀態
// }

// // ❌ 這樣不會有效果
// <motion.div
//   variants={variants}
//   initial="initial"
//   whileHover={{ scale: 1.2 }} // 這會被 variants 覆蓋
// >

// // ✅ 正確做法
// <motion.div
//   variants={variants}
//   initial="initial"
//   whileHover="hover" // 使用 variants 中定義的 hover 狀態
// >

import { hover, motion } from "motion-v";
import { ref } from "vue";

// 控制每個範例動畫播放的狀態
const isAnimating1 = ref(false); // 卡片網格動畫
const isAnimating2 = ref(false); // 列表項目動畫
const isAnimating3 = ref(false); // 按鈕組動畫

// 容器動畫變體配置
// staggerChildren: 控制子元素動畫的延遲間隔
const containerVariants = {
  hidden: {
    opacity: 0
  },
  visible: {
    opacity: 1,
    transition: {
      // staggerChildren: 每個子元素動畫延遲 0.2 秒
      staggerChildren: 0.2,
      // delayChildren: 容器動畫完成後延遲 0.1 秒再開始子元素動畫
      delayChildren: 0.1
    }
  }
};

// 子元素動畫變體配置
const itemVariants = {
  hidden: {
    y: 50,        // 從下方 50px 開始
    opacity: 0,   // 完全透明
    scale: 0.8    // 縮小到 80%
  },
  visible: {
    y: 0,         // 移動到原位置
    opacity: 1,   // 完全不透明
    scale: 1,     // 恢復原始大小
    transition: {
      type: "spring",  // 使用彈簧動畫
      stiffness: 100,  // 彈簧剛度
      damping: 12      // 阻尼係數
    },
  },
  hover: {
    scale: 1.3, // 滑鼠懸停時放大
    transition: {
      type: "spring",
      stiffness: 200,
      damping: 15
    }
  }
};

// 卡片數據配置
const cards = [
  { id: 1, title: "第一張卡片", desc: "我會第一個出現", color: "#ff0088", icon: "🎯" },
  { id: 2, title: "第二張卡片", desc: "我會延遲 0.2 秒", color: "#4ff0b7", icon: "🚀" },
  { id: 3, title: "第三張卡片", desc: "我會延遲 0.4 秒", color: "#0d63f8", icon: "⭐" },
  { id: 4, title: "第四張卡片", desc: "我會延遲 0.6 秒", color: "#f7b801", icon: "🎨" },
  { id: 5, title: "第五張卡片", desc: "我會延遲 0.8 秒", color: "#9c27b0", icon: "🎪" },
  { id: 6, title: "第六張卡片", desc: "我會延遲 1.0 秒", color: "#ff5722", icon: "🎭" }
];

// 列表項目數據配置（用於第二個範例）
const listItems = [
  "使用 staggerChildren 可以讓子元素依序動畫",
  "每個子元素會根據設定的延遲時間依序播放",
  "這樣可以創造出波浪式的動畫效果",
  "非常適合用於列表、網格或導航選單",
  "可以搭配不同的動畫效果使用"
];

// 第二個範例：列表容器動畫變體配置
const listContainerVariants = {
  hidden: {
    opacity: 0
  },
  visible: {
    opacity: 1,
    transition: {
      staggerChildren: 0.15, // 更快的錯開間隔
      delayChildren: 0.2     // 容器動畫完成後延遲 0.2 秒
    }
  }
};

// 第二個範例：列表項目動畫變體配置
const listItemVariants = {
  hidden: {
    x: -100,      // 從左側滑入
    opacity: 0,
    rotateY: -90  // 3D 旋轉效果
  },
  visible: {
    x: 0,
    opacity: 1,
    rotateY: 0,
    transition: {
      type: 'spring', // 使用彈簧動畫
      stiffness: 120, // 彈簧剛度
      damping: 15 // 阻尼係數
    }
  }
};

// 第三個範例：按鈕容器動畫變體配置
const buttonContainerVariants = {
  hidden: {
    scale: 0.8,
    opacity: 0
  },
  visible: {
    scale: 1,
    opacity: 1,
    transition: {
      staggerChildren: 0.1,  // 快速錯開
      delayChildren: 0.3,    // 延遲 0.3 秒開始
      type: 'spring',
      stiffness: 200
    }
  }
};

// 第三個範例：按鈕項目動畫變體配置
const buttonItemVariants = {
  hidden: {
    y: -30,       // 從上方滑入
    opacity: 0,
    scale: 0.1    // 從小尺寸開始
  },
  visible: {
    y: 0,
    opacity: 1,
    scale: 1,
    transition: {
      type: 'spring',
      stiffness: 300,
      damping: 20
    }
  },
};

// 觸發動畫的函數
const triggerAnimation1 = () => {
  isAnimating1.value = false;
  setTimeout(() => {
    isAnimating1.value = true;
  }, 50);
};

const triggerAnimation2 = () => {
  isAnimating2.value = false;
  setTimeout(() => {
    isAnimating2.value = true;
  }, 50);
};

const triggerAnimation3 = () => {
  isAnimating3.value = false;
  setTimeout(() => {
    isAnimating3.value = true;
  }, 50);
};

// 重置動畫的函數
const resetAnimation1 = () => {
  isAnimating1.value = false;
};

const resetAnimation2 = () => {
  isAnimating2.value = false;
};

const resetAnimation3 = () => {
  isAnimating3.value = false;
};
</script>

<template>
  <div class="motion-10-container">
    <!-- 標題區域 -->
    <div class="header-section">
      <h1 class="main-title">
        staggerChildren 錯開動畫範例
      </h1>
      <p class="main-desc">
        展示如何使用 staggerChildren 讓多個子元素依序播放動畫，創造出優雅的波浪式效果
      </p>
    </div>

    <!-- 第一個範例：卡片網格動畫 -->
    <section class="example-section">
      <h2 class="section-title">
        範例一：卡片網格錯開動畫
      </h2>
      <p class="section-desc">
        使用 staggerChildren: 0.2 讓每張卡片延遲 0.2 秒依序出現
      </p>

      <!-- 範例一控制按鈕 -->
      <div class="example-controls">
        <button
          class="trigger-btn"
          @click="triggerAnimation1"
        >
          🎬 播放卡片動畫
        </button>
        <button
          class="reset-btn"
          @click="resetAnimation1"
        >
          🔄 重置
        </button>
      </div>

      <!--
        motion.div 作為容器，設定 variants 和 staggerChildren
        :animate 根據 isAnimating 狀態切換動畫
      -->
      <motion.div
        class="cards-container"
        :variants="containerVariants"
        :initial="'hidden'"
        :animate="isAnimating1 ? 'visible' : 'hidden'"
        :while-hover="'hover'"
      >
        <!--
          每個子元素都會自動應用 staggerChildren 的延遲效果
          不需要手動設定每個元素的延遲時間
        -->
        <motion.div
          v-for="card in cards"
          :key="card.id"
          class="card"
          :variants="itemVariants"
          :style="{ '--card-color': card.color }"
        >
          <div class="card-icon">
            {{ card.icon }}
          </div>
          <h3 class="card-title">
            {{ card.title }}
          </h3>
          <p class="card-desc">
            {{ card.desc }}
          </p>
        </motion.div>
      </motion.div>
    </section>

    <!-- 第二個範例：列表項目錯開動畫 -->
    <section class="example-section">
      <h2 class="section-title">
        範例二：列表項目錯開動畫
      </h2>
      <p class="section-desc">
        展示不同的動畫效果搭配 staggerChildren 的使用
      </p>

      <!-- 範例二控制按鈕 -->
      <div class="example-controls">
        <button
          class="trigger-btn"
          @click="triggerAnimation2"
        >
          🎬 播放列表動畫
        </button>
        <button
          class="reset-btn"
          @click="resetAnimation2"
        >
          🔄 重置
        </button>
      </div>

      <!--
        這個範例使用不同的動畫變體
        展示 staggerChildren 的靈活性
      -->
      <motion.ul
        class="list-container"
        :variants="listContainerVariants"
        :initial="'hidden'"
        :animate="isAnimating2 ? 'visible' : 'hidden'"
      >
        <motion.li
          v-for="(item, index) in listItems"
          :key="index"
          class="list-item"
          :variants="listItemVariants"
        >
          <span class="list-number">{{ String(index + 1).padStart(2, '0') }}</span>
          <span class="list-text">{{ item }}</span>
        </motion.li>
      </motion.ul>
    </section>

    <!-- 第三個範例：按鈕組錯開動畫 -->
    <section class="example-section">
      <h2 class="section-title">
        範例三：按鈕組錯開動畫
      </h2>
      <p class="section-desc">
        展示導航按鈕或工具列的錯開動畫效果
      </p>

      <!-- 範例三控制按鈕 -->
      <div class="example-controls">
        <button
          class="trigger-btn"
          @click="triggerAnimation3"
        >
          🎬 播放按鈕動畫
        </button>
        <button
          class="reset-btn"
          @click="resetAnimation3"
        >
          🔄 重置
        </button>
      </div>

      <motion.div
        class="buttons-container"
        :variants="buttonContainerVariants"
        :initial="'hidden'"
        :animate="isAnimating3 ? 'visible' : 'hidden'"
      >
        <motion.button
          v-for="(btn, index) in ['首頁', '關於', '服務', '作品', '聯絡']"
          :key="index"
          class="nav-button"
          :variants="buttonItemVariants"
        >
          {{ btn }}
        </motion.button>
      </motion.div>
    </section>

    <!-- 程式碼說明區域 -->
    <section class="code-explanation">
      <h2 class="section-title">
        💡 staggerChildren 重點說明
      </h2>
      <div class="explanation-grid">
        <div class="explanation-card">
          <h3>🎯 什麼是 staggerChildren</h3>
          <p>
            staggerChildren 是 Motion 中用來控制子元素動畫延遲的屬性。
            它會讓每個子元素依序播放動畫，而不是同時開始。
          </p>
        </div>

        <div class="explanation-card">
          <h3>⏱️ 延遲時間計算</h3>
          <p>
            如果設定 staggerChildren: 0.2，第一個子元素延遲 0s，
            第二個延遲 0.2s，第三個延遲 0.4s，以此類推。
          </p>
        </div>

        <div class="explanation-card">
          <h3>🔧 搭配 delayChildren</h3>
          <p>
            delayChildren 可以讓所有子元素在容器動畫完成後，
            再統一延遲一段時間才開始播放。
          </p>
        </div>

        <div class="explanation-card">
          <h3>🎨 應用場景</h3>
          <p>
            適合用於列表項目、卡片網格、導航選單、
            圖片畫廊等需要依序出現的元素組合。
          </p>
        </div>
      </div>
    </section>
  </div>
</template>

<style scoped>
.motion-10-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 2rem;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
}

/* 標題區域樣式 */
.header-section {
  text-align: center;
  margin-bottom: 4rem;
  padding: 2rem;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  border-radius: 20px;
  color: white;
}

.main-title {
  font-size: 2.5rem;
  margin-bottom: 1rem;
  font-weight: 700;
}

.main-desc {
  font-size: 1.2rem;
  margin-bottom: 2rem;
  opacity: 0.9;
  line-height: 1.6;
}

/* 控制按鈕樣式 */
.controls, .example-controls {
  display: flex;
  gap: 1rem;
  justify-content: center;
  flex-wrap: wrap;
  margin-bottom: 2rem;
}

.trigger-btn, .reset-btn {
  padding: 12px 24px;
  border: none;
  border-radius: 50px;
  font-size: 1rem;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
}

.trigger-btn {
  background: linear-gradient(45deg, #ff0088, #ff4081);
  color: white;
}

.trigger-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(255, 0, 136, 0.4);
}

.reset-btn {
  background: linear-gradient(45deg, #4ff0b7, #00bcd4);
  color: white;
}

.reset-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(79, 240, 183, 0.4);
}

/* 區段樣式 */
.example-section {
  margin-bottom: 4rem;
  padding: 2rem;
  background: rgba(255, 255, 255, 0.05);
  border-radius: 16px;
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.1);
}

.section-title {
  font-size: 1.8rem;
  margin-bottom: 0.5rem;
  color: #333;
  font-weight: 600;
}

.section-desc {
  font-size: 1rem;
  color: #666;
  margin-bottom: 2rem;
  line-height: 1.6;
}

/* 卡片網格樣式 */
.cards-container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 1.5rem;
  margin-top: 2rem;
}

.card {
  background: white;
  padding: 2rem;
  border-radius: 16px;
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
  text-align: center;
  border: 2px solid var(--card-color);
  position: relative;
  overflow: hidden;
}

.card::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 4px;
  background: var(--card-color);
}

.card-icon {
  font-size: 3rem;
  margin-bottom: 1rem;
}

.card-title {
  font-size: 1.3rem;
  margin-bottom: 0.5rem;
  color: #333;
  font-weight: 600;
}

.card-desc {
  color: #666;
  font-size: 0.95rem;
  line-height: 1.5;
}

/* 列表樣式 */
.list-container {
  list-style: none;
  padding: 0;
  margin: 2rem 0;
}

.list-item {
  display: flex;
  align-items: center;
  padding: 1rem 1.5rem;
  margin-bottom: 1rem;
  background: white;
  border-radius: 12px;
  box-shadow: 0 4px 16px rgba(0, 0, 0, 0.1);
  border-left: 4px solid #ff0088;
}

.list-number {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 32px;
  height: 32px;
  background: linear-gradient(45deg, #ff0088, #ff4081);
  color: white;
  border-radius: 50%;
  font-weight: 600;
  font-size: 0.9rem;
  margin-right: 1rem;
  flex-shrink: 0;
}

.list-text {
  font-size: 1rem;
  color: #333;
  line-height: 1.5;
}

/* 按鈕組樣式 */
.buttons-container {
  display: flex;
  gap: 1rem;
  justify-content: center;
  flex-wrap: wrap;
  margin-top: 2rem;
}

.nav-button {
  padding: 12px 24px;
  border: none;
  border-radius: 50px;
  background: linear-gradient(45deg, #667eea, #764ba2);
  color: white;
  font-size: 1rem;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 0 4px 15px rgba(102, 126, 234, 0.3);
}

.nav-button:hover {
  box-shadow: 0 6px 20px rgba(102, 126, 234, 0.4);
}

/* 說明區域樣式 */
.code-explanation {
  margin-top: 4rem;
  padding: 2rem;
  background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
  border-radius: 20px;
}

.explanation-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 1.5rem;
  margin-top: 2rem;
}

.explanation-card {
  background: white;
  padding: 1.5rem;
  border-radius: 12px;
  box-shadow: 0 4px 16px rgba(0, 0, 0, 0.1);
}

.explanation-card h3 {
  font-size: 1.2rem;
  margin-bottom: 1rem;
  color: #333;
  font-weight: 600;
}

.explanation-card p {
  color: #666;
  line-height: 1.6;
  font-size: 0.95rem;
}

/* 響應式設計 */
@media (max-width: 768px) {
  .motion-10-container {
    padding: 1rem;
  }

  .main-title {
    font-size: 2rem;
  }

  .cards-container {
    grid-template-columns: 1fr;
  }

  .buttons-container {
    flex-direction: column;
    align-items: center;
  }

  .nav-button {
    width: 200px;
  }
}
</style>
