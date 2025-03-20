<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
import { onMounted, ref } from 'vue'
import ParticlesBackground from './components/ParticlesBackground.vue'

const isTyping = ref(false)
const text = ref('')
const fullText = '欢迎来到琦总的个人网站！'

onMounted(() => {
  isTyping.value = true
  let currentIndex = 0
  const typingInterval = setInterval(() => {
    if (currentIndex < fullText.length) {
      text.value += fullText[currentIndex]
      currentIndex++
    } else {
      clearInterval(typingInterval)
      isTyping.value = false
    }
  }, 200)
})
</script>

<template>
  <div class="app-container">
    <ParticlesBackground />

    <header class="glass-header">
      <nav>
        <RouterLink to="/" class="nav-link">首页</RouterLink>
        <RouterLink to="/about" class="nav-link">关于</RouterLink>
        <RouterLink to="/blog" class="nav-link">博客</RouterLink>
      </nav>
    </header>

    <main class="main-content">
      <div class="hero-section">
        <h1 class="typing-text">{{ text }}<span v-if="isTyping" class="cursor">|</span></h1>
        <p class="subtitle">探索、创造、分享</p>
      </div>

      <div class="cards-container">
        <div class="card" v-for="i in 3" :key="i">
          <div class="card-content">
            <h3>创意 {{ i }}</h3>
            <p>这是一个充满创意的卡片，展示你的独特想法。</p>
          </div>
        </div>
      </div>
    </main>

    <RouterView />
  </div>
</template>

<style scoped>
.app-container {
  min-height: 100vh;
  position: relative;
  overflow: hidden;
}

.glass-header {
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(10px);
  padding: 1rem 2rem;
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 100;
}

nav {
  display: flex;
  justify-content: center;
  gap: 2rem;
}

.nav-link {
  color: #fff;
  text-decoration: none;
  font-size: 1.1rem;
  position: relative;
  padding: 0.5rem 1rem;
  transition: all 0.3s ease;
}

.nav-link::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 0;
  width: 0;
  height: 2px;
  background: linear-gradient(90deg, #ff6b6b, #4ecdc4);
  transition: width 0.3s ease;
}

.nav-link:hover::after {
  width: 100%;
}

.main-content {
  padding-top: 100px;
  text-align: center;
}

.hero-section {
  margin-bottom: 4rem;
}

.typing-text {
  font-size: 3rem;
  color: #fff;
  margin-bottom: 1rem;
}

.cursor {
  animation: blink 1s infinite;
}

.subtitle {
  font-size: 1.5rem;
  color: #4ecdc4;
  margin-bottom: 2rem;
}

.cards-container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 2rem;
  padding: 2rem;
  max-width: 1200px;
  margin: 0 auto;
}

.card {
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(10px);
  border-radius: 15px;
  padding: 2rem;
  transform-style: preserve-3d;
  transition: transform 0.3s ease;
  cursor: pointer;
}

.card:hover {
  transform: translateY(-10px) rotateX(5deg);
}

.card-content {
  color: #fff;
}

.card h3 {
  font-size: 1.5rem;
  margin-bottom: 1rem;
  background: linear-gradient(90deg, #ff6b6b, #4ecdc4);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

@keyframes blink {

  0%,
  100% {
    opacity: 1;
  }

  50% {
    opacity: 0;
  }
}

@media (max-width: 768px) {
  .typing-text {
    font-size: 2rem;
  }

  .subtitle {
    font-size: 1.2rem;
  }

  .cards-container {
    grid-template-columns: 1fr;
  }
}
</style>
