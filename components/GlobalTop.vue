<script setup lang="ts">
import { computed } from 'vue'
import { useRoute } from 'vue-router'
import { useNav } from '@slidev/client'

const route = useRoute()
const { total } = useNav()
const currentPage = computed(() => Number(route.path.match(/\/(\d+)\/?$/)?.[1] ?? 1))
</script>

<template>
  <div class="course-header">Redes y comunicaciones - Facultad de Informática - UNLP</div>
  <div class="slide-counter">{{ currentPage }} / {{ total }}</div>
</template>

<style scoped>
.course-header {
  position: absolute;
  top: 0.55rem;
  right: 1rem;
  z-index: 20;
  color: #64748b;
  font-size: 0.62em;
  font-weight: 500;
  pointer-events: none;
}

.slide-counter {
  position: fixed;
  right: 0.75rem;
  bottom: 0.45rem;
  z-index: 30;
  padding: 0.25rem 0.55rem;
  border-radius: 2px;
  background: rgb(245 245 245 / 92%);
  color: #475569;
  font-family: monospace;
  font-size: 0.58em;
  pointer-events: none;
}
</style>

<style>
.slidev-page footer > .absolute.bottom-0.right-0 {
  visibility: hidden;
}
</style>
