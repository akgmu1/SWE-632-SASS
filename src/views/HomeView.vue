<script setup lang="ts">
import { ref, type Ref } from 'vue'

interface Item {
  id: number
  value: number
}

type CreateItem = Omit<Item, 'id'>

let id = 0
const list: Ref<Item[]> = ref([])
const input = ref('')
const error = ref('')

function addItem(item: CreateItem) {
  list.value.push({
    ...item,
    id: id++,
  })
}

const DEFAULT_ITEMS = [1, 2, 3, 4, 5] as const

for (const x of DEFAULT_ITEMS) {
  addItem({ value: x })
}

function onClick() {
  const x = Number(input.value)
  if (input.value.length > 0 && !Number.isNaN(x)) {
    addItem({ value: x })
    input.value = ''
    error.value = ''
  } else {
    error.value = 'Input was not a number or empty'
  }
}
</script>

<template>
  <main>
    <header>My Application</header>
    <div class="top">
      <div class="form-group">
        <label> Number </label>
        <input v-model="input" type="text" placeholder="Enter Number..." @keydown.enter="onClick" />
        <button class="btn btn-primary" @click="onClick">Add</button>
      </div>
      <div v-if="error" class="text-danger">
        {{ error }}
      </div>
    </div>
    <div class="items">
      <div v-for="x in list" :key="x.id">
        <div class="item">
          <div>{{ x.value }}</div>
          <button
            class="btn-sm btn-danger"
            @click="
              () => {
                list = list.filter((e) => e.id !== x.id)
              }
            "
          >
            Remove
          </button>
        </div>
      </div>
    </div>
    <div class="bottom">
      <button
        class="btn btn-primary"
        @click="
          () => {
            list = list.sort((a, b) => a.value - b.value)
          }
        "
      >
        Sort
      </button>
      <button
        class="btn btn-secondary"
        @click="
          () => {
            list = list.sort(() => Math.random() - 0.5)
          }
        "
      >
        Randomize
      </button>
    </div>
  </main>
</template>

<style lang="scss" scoped>
@use '@/styles' as *;

.form-group {
  margin-bottom: 0.5rem;
}

header {
  background-color: $primary-bg;
  color: $primary-fg;
  margin-bottom: 1rem;
  font-size: $font-2xl;
  text-align: center;
  padding-bottom: 0.5rem;
}

.top {
  @include flex-center;
  flex-direction: column;
  margin-bottom: 1rem;
}

.items {
  @include flex-center;
  flex-direction: column;
  gap: spacing(1);
}

.item {
  background-color: $bg-alt;
  padding: 0.5rem;
  @include rounded;

  @include flex-center;
  gap: spacing(1);
}

.bottom {
  @include flex-center;
  gap: spacing(3);
  margin-top: 1rem;
}
</style>
