<script setup lang="ts">
import TheHeader from './TheHeader.vue'
import TheSidebar from './TheSidebar.vue'
import TheFooter from './TheFooter.vue'
import { BackgroundRender } from '@applemusic-like-lyrics/vue';
import { ref } from 'vue';
//随机图片
const randomImage = Math.floor(Math.random() * 3) + 1;
const imageUrl = ref(`https://picsum.photos/1920/1080?random=${randomImage}`);

</script>

<template>
  <div class="layout-container">
    <div class="full-page-background">
      <BackgroundRender :album="imageUrl" />
    </div>
    <TheHeader class="header" />
    <TheSidebar class="sidebar" />
    <main class="main">
      <slot />
    </main>
    <TheFooter class="footer" />
  </div>
</template>

<style scoped>
.layout-container {
  display: grid;
  grid-template-areas:
    "header header"
    "sidebar main";
  grid-template-rows: auto 1fr;
  grid-template-columns: auto 1fr;
  height: 100vh;
  padding-bottom: 80px;
  /* 为固定底部播放器留出空间 */
  overflow: hidden;
  position: relative;
}

.full-page-background {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(135deg, rgba(231, 76, 60, 0.05) 0%, rgba(192, 57, 43, 0.05) 100%);
  pointer-events: none;
  z-index: 1;
}


.header {
  grid-area: header;
  position: sticky;
  top: 0;
  z-index: 100;
  background-color: #fff;
  /* Opaque background to hide the full page background */
}

.sidebar {
  grid-area: sidebar;
  overflow-y: auto;
  height: calc(100vh - 60px);
  /* 减去header高度 */
  background-color: #f8f9fa;
  /* Opaque background to hide the full page background */
  position: relative;
  z-index: 2;
}

.main {
  grid-area: main;
  overflow-y: auto;
  height: calc(100vh - 60px);
  /* 减去header高度 */
  padding: 20px 20px 100px 20px;
  /* 底部增加80px padding避免被footer挡住 */
  position: relative;
  z-index: 2;
  /* Main content area will show the full page background */
}

.footer {
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  z-index: 99;
  background-color: #2c2c2c;
  /* Opaque background to hide the full page background */
}
</style>