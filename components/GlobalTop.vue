<script setup lang="ts">
import { computed } from 'vue'
import { useRoute } from 'vue-router'
import { useNav } from '@slidev/client'

const route = useRoute()
const { total } = useNav()
const currentPage = computed(() => Number(route.path.match(/\/(\d+)\/?$/)?.[1] ?? 1))
</script>

<template>
  <div class="edge-tint" aria-hidden="true" />
  <img class="edge-decoration" src="../images/edge-network.svg" alt="" aria-hidden="true">
  <div class="course-header">Redes y comunicaciones - Facultad de Informática - UNLP</div>
  <div class="slide-counter">{{ currentPage }} / {{ total }}</div>
</template>

<style scoped>
.edge-tint {
  position: absolute;
  inset: 0;
  z-index: 0;
  background:
    linear-gradient(90deg, rgb(145 211 235 / 42%) 0%, rgb(196 231 245 / 24%) 4%, transparent 13%, transparent 87%, rgb(196 231 245 / 24%) 96%, rgb(145 211 235 / 42%) 100%),
    linear-gradient(180deg, rgb(176 224 241 / 20%) 0%, transparent 14%, transparent 86%, rgb(176 224 241 / 20%) 100%);
  pointer-events: none;
}

.edge-decoration {
  position: absolute;
  inset: 0;
  z-index: 0;
  width: 100%;
  height: 100%;
  object-fit: fill;
  pointer-events: none;
  user-select: none;
}

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
