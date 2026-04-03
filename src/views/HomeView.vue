<script setup lang="ts">
import { ref } from 'vue'

const list = ref([1, 2, 3, 4, 5])
</script>

<template>
  <main>
    <header>Hello</header>
    <div class="items">
      <div v-for="x in list">
        <div class="item">{{ x }}</div>
      </div>
    </div>
  </main>
</template>

<style lang="scss" scoped>
@use '@/styles' as *;

header {
  font-size: $font-2xl;
  background-color: $primary;
  color: $bg-color;
  margin-bottom: rem(20);
  padding-bottom: rem(10);
  text-align: center;
}

.items {
  @include flex-center;
  gap: 1rem;
}

.item {
  background-color: $fg-color;
  color: $bg-color;
  border-radius: rem(5);
  padding: 0.5rem;

  &:hover {
    background-color: $primary;
    color: $bg-color;
  }
}
</style>
