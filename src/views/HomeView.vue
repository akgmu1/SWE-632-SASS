<script setup lang="ts">
import { ref } from 'vue'

const list = ref([1, 2, 3, 4, 5])
</script>

<template>
  <main>
    <header>Hello</header>
    <div
      class="items"
      :style="{
        'margin-bottom': '1rem',
      }"
    >
      <div v-for="x in list">
        <div class="item">{{ x }}</div>
      </div>
    </div>
    <div class="items">
      <button class="btn btn-outline">Action A</button>
      <button class="btn btn-primary">Action B</button>
      <button class="btn btn-outline-primary">Action B</button>
    </div>
  </main>
</template>

<style lang="scss" scoped>
@use '@/styles' as *;

header {
  font-size: $font-2xl;
  text-align: center;

  background-color: $primary-color;
  color: $bg-color;

  margin-bottom: 1rem;
  padding-bottom: 0.5rem;
}

.items {
  @include flex-center;
  gap: 1rem;
}

.item {
  background-color: $fg-color;
  color: $bg-color;

  @include round;
  padding: 0.5rem;

  &:hover {
    background-color: $primary-color;
    color: $bg-color;
  }
}
</style>
