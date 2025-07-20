<script setup>
import { ref } from 'vue'
import Motion01 from './components/motion-01.vue'
import Motion02 from './components/motion-02.vue'
import Motion03 from './components/motion-03.vue'
import Motion04 from './components/motion-04.vue'
import Motion05 from './components/motion-05.vue'
import Motion06 from './components/motion-06.vue'
import Motion07 from './components/motion-07.vue'

const currentComponent = ref(null)

const motionExamples = [
  {
    id: 'motion-01',
    title: '基本動畫控制',
    description: '使用滑桿控制元素的位置和旋轉',
    component: Motion01
  },
  {
    id: 'motion-02',
    title: 'SVG 路徑動畫',
    description: '展示 SVG 路徑繪製動畫效果',
    component: Motion02
  },
  {
    id: 'motion-03',
    title: '球體彈跳動畫',
    description: '展示球體的彈跳動畫效果',
    component: Motion03
  },
  {
    id: 'motion-04',
    title: '進出場動畫',
    description: '展示元素的進出場動畫效果',
    component: Motion04
  },
  {
    id: 'motion-05',
    title: '關鍵幀動畫',
    description: '展示關鍵幀動畫效果',
    component: Motion05
  },
  {
    id: 'motion-06',
    title: '懸停動畫',
    description: '展示元素在懸停時的動畫效果',
    component: Motion06
  },
  {
    id: 'motion-07',
    title: '縮放和按壓動畫',
    description: '展示元素在懸停和按壓時的縮放效果',
    component: Motion07
  }
]

const showExample = (example) => {
  currentComponent.value = example
}

const backToHome = () => {
  currentComponent.value = null
}
</script>

<template>
  <div class="app">
    <!-- 主頁：案例清單 -->
    <div v-if="!currentComponent" class="home">
      <header class="header">
        <div class="logos">
          <a href="https://vite.dev" target="_blank">
            <img src="/vite.svg" class="logo" alt="Vite logo" />
          </a>
          <a href="https://vuejs.org/" target="_blank">
            <img src="./assets/vue.svg" class="logo vue" alt="Vue logo" />
          </a>
        </div>
        <h1>Motion-V 案例展示</h1>
        <p>點擊下方案例來查看不同的動畫效果</p>
      </header>

      <div class="examples-grid">
        <div
          v-for="example in motionExamples"
          :key="example.id"
          class="example-card"
          @click="showExample(example)"
        >
          <h3>{{ example.title }}</h3>
          <p>{{ example.description }}</p>
          <div class="view-btn">查看案例</div>
        </div>
      </div>
    </div>

    <!-- 案例詳情頁 -->
    <div v-else class="example-detail">
      <header class="detail-header">
        <button class="back-btn" @click="backToHome">
          ← 返回主頁
        </button>
        <h2>{{ currentComponent.title }}</h2>
      </header>

      <div class="example-content">
        <component :is="currentComponent.component" />
      </div>
    </div>
  </div>
</template>

<style scoped>
.app {
  min-height: 100vh;
  padding: 20px;
}

/* 主頁樣式 */
.home {
  max-width: 1200px;
  margin: 0 auto;
}

.header {
  text-align: center;
  margin-bottom: 3rem;
}

.logos {
  display: flex;
  justify-content: center;
  gap: 20px;
  margin-bottom: 2rem;
}

.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}

.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}

.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}

.header h1 {
  font-size: 3rem;
  margin-bottom: 1rem;
  background: linear-gradient(45deg, #646cff, #42b883);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.header p {
  font-size: 1.2rem;
  color: #666;
}

/* 案例網格 */
.examples-grid {
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  gap: 1rem;
  margin-top: 2rem;
}

/* 響應式布局 */
@media (max-width: 1200px) {
  .examples-grid {
    grid-template-columns: repeat(4, 1fr);
  }
}

@media (max-width: 900px) {
  .examples-grid {
    grid-template-columns: repeat(3, 1fr);
  }
}

@media (max-width: 600px) {
  .examples-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 400px) {
  .examples-grid {
    grid-template-columns: 1fr;
  }
}

.example-card {
  background: #fff;
  border-radius: 8px;
  padding: 1.2rem;
  border: 2px solid #e5e7eb;
  transition: all 0.3s ease;
  cursor: pointer;
  position: relative;
  overflow: hidden;
  text-align: center;
  min-height: 140px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.example-card:hover {
  border-color: #646cff;
  transform: translateY(-4px);
  box-shadow: 0 8px 25px rgba(100, 108, 255, 0.15);
}

.example-card h3 {
  font-size: 1.1rem;
  margin-bottom: 0.5rem;
  color: #1f2937;
}

.example-card p {
  color: #6b7280;
  margin-bottom: 1rem;
  line-height: 1.4;
  font-size: 0.85rem;
}

.view-btn {
  display: inline-block;
  background: linear-gradient(45deg, #646cff, #42b883);
  color: white;
  padding: 0.5rem 1rem;
  border-radius: 6px;
  font-weight: 600;
  font-size: 0.85rem;
  transition: transform 0.2s ease;
}

.example-card:hover .view-btn {
  transform: scale(1.05);
}

/* 案例詳情頁樣式 */
.example-detail {
  max-width: 1200px;
  margin: 0 auto;
}

.detail-header {
  display: flex;
  align-items: center;
  gap: 1rem;
  margin-bottom: 2rem;
  padding-bottom: 1rem;
  border-bottom: 2px solid #e5e7eb;
}

.back-btn {
  background: #646cff;
  color: white;
  border: none;
  padding: 0.75rem 1.5rem;
  border-radius: 8px;
  cursor: pointer;
  font-size: 1rem;
  transition: background-color 0.2s ease;
}

.back-btn:hover {
  background: #5855d1;
}

.detail-header h2 {
  font-size: 2rem;
  color: #1f2937;
  margin: 0;
}

.example-content {
  background: #f9fafb;
  border-radius: 12px;
  padding: 2rem;
  min-height: 500px;
}

/* 深色模式支援 */
@media (prefers-color-scheme: dark) {
  .app {
    background: #1a1a1a;
    color: #e5e7eb;
  }

  .example-card {
    background: #2d3748;
    border-color: #4a5568;
  }

  .example-card h3 {
    color: #e5e7eb;
  }

  .example-card p {
    color: #a0aec0;
  }

  .detail-header {
    border-color: #4a5568;
  }

  .detail-header h2 {
    color: #e5e7eb;
  }

  .example-content {
    background: #2d3748;
  }
}
</style>
