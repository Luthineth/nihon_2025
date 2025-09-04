<template>
  <div class="floating-nav" v-show="showButton">
    <button class="nav-button" @click="scrollToTop">↑</button>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'

const showButton = ref(false)

const scrollToTop = () => {
  window.scrollTo({ top: 0, behavior: 'smooth' })
}

const handleScroll = () => {
  showButton.value = window.scrollY > 300
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<style scoped>
.floating-nav {
  position: fixed;
  bottom: 2rem;
  right: 2rem;
  z-index: 100;
}

.nav-button {
  background: linear-gradient(45deg, #667eea, #764ba2);
  color: white;
  border: none;
  border-radius: 50%;
  width: 60px;
  height: 60px;
  font-size: 1.5rem;
  cursor: pointer;
  box-shadow: 0 10px 30px rgba(102, 126, 234, 0.3);
  transition: all 0.3s ease;
}

.nav-button:hover {
  transform: scale(1.1);
  box-shadow: 0 15px 40px rgba(102, 126, 234, 0.4);
}

.nav-button:active {
  transform: translateY(0);
}
</style>