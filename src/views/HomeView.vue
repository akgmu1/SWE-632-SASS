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
</script>

<template>
  <main>
    <header>My Application</header>
    <div>
      <label> Number </label>
      <input v-model="input" type="text" placeholder="Enter Number..." />
      <div v-if="error">
        {{ error }}
      </div>
      <button
        @click="
          () => {
            const x = Number(input)
            if (input.length > 0 && !Number.isNaN(x)) {
              addItem({ value: x })
              input = ''
              error = ''
            } else {
              error = 'Input was not a number or empty'
            }
          }
        "
      >
        Add
      </button>
    </div>
    <div>
      <div v-for="x in list" :key="x.id">
        <div>{{ x.value }}</div>
        <button
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
    <div>
      <button
        @click="
          () => {
            list = list.sort((a, b) => a.value - b.value)
          }
        "
      >
        Sort
      </button>
      <button
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
</style>
