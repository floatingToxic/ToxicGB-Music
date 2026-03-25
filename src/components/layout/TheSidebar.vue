<script setup lang="ts">
import NavigationMenu from '../common/NavigationMenu.vue'
import type { MenuItem } from '@/types/menu'

defineProps<{
  isCollapsed?: boolean
}>()

defineEmits<{
  'update:isCollapsed': [value: boolean]
}>()

const menuItems: MenuItem[] = [
  {
    id: 'home',
    label: '首页',
    icon: '🏠',
    route: '/'
  },
  {
    id: 'search',
    label: '搜索',
    icon: '🔍',
    route: '/search'
  },
  {
    id: 'playlists',
    label: '歌单',
    icon: '📋',
    children: [
      {
        id: 'my-playlists',
        label: '我的歌单',
        route: '/playlists/my'
      },
    ]
  },
]
</script>

<template>
  <aside class="sidebar" :class="{ collapsed: isCollapsed }">
    <NavigationMenu :items="menuItems" />
  </aside>
</template>

<style scoped>
.sidebar {
  width: 240px;
  background-color: #f8f9fa;
  border-right: 1px solid #e0e0e0;
  transition: width 0.3s ease;
}

.sidebar.collapsed {
  width: 60px;
}

@media (max-width: 768px) {
  .sidebar {
    position: fixed;
    left: -240px;
    z-index: 99;
    height: calc(100vh - 60px);
  }

  .sidebar.open {
    left: 0;
  }
}
</style>