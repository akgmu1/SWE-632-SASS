<script setup lang="ts">
import { ref } from 'vue'

const list = ref([1, 2, 3, 4, 5])
</script>

<template>
  <main>
    <div class="header">Hello</div>
    <div class="items">
      <div v-for="x in list">
        <div class="item">{{ x }}</div>
      </div>
    </div>
  </main>
</template>

<style lang="scss" scoped>
@use '@/assets/_mixins.scss' as *;

.header {
  font-size: 5rem;
}

.items {
  @include flex-center;
  gap: 1rem;
}

.item {
  font-size: 1rem;
  background-color: blue;
  color: white;
  border-radius: 1rem;
  padding: 0.5rem;

  &:hover {
    background-color: aquamarine;
  }
}
</style>
