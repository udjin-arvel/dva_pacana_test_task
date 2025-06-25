<template>
  <div class="container mx-auto p-4">
    <h1 class="text-2xl font-bold mb-6">Тестовое</h1>

    <div class="flex mb-8 gap-4">
      <div class="flex-1 border rounded p-4">
        <h2 class="text-xl font-semibold mb-4">Выбранные элементы (до 4)</h2>
        <div class="flex flex-wrap gap-2 min-h-20">
          <div
              v-for="(item, index) in selectedLeftItems"
              :key="'selected-user-' + index"
              @click="removeLeftItem(index)"
              class="cursor-pointer bg-green-100 border-green-300 border rounded p-2"
          >
            {{ item.name }} ({{ item.id }})
          </div>
          <div v-if="selectedLeftItems.length === 0" class="text-gray-400">
            Элементы не выбраны
          </div>
        </div>
      </div>

      <div class="flex-1 border rounded p-4">
        <h2 class="text-xl font-semibold mb-4">Выбранный элемент</h2>
        <div class="min-h-20">
          <div
              @click="selectRightItem(selectedRightItem)"
              v-if="selectedRightItem"
              class="cursor-pointer bg-purple-100 border-purple-300 border rounded p-2"
          >
            {{ selectedRightItem.name }} ({{ selectedRightItem.id }})
          </div>
          <div v-else class="text-gray-400">
            Элемент не выбран
          </div>
        </div>
      </div>
    </div>

    <div class="flex gap-4">
      <div class="flex-1 border rounded p-4">
        <h2 class="text-xl font-semibold mb-4">Список 1</h2>
        <div class="grid grid-cols-3 gap-2">
          <Item
              v-for="item in leftItems"
              :key="'user-' + item.id"
              :item="item"
              :selected="selectedLeftItems.some(i => i.id === item.id)"
              @select="selectLeftItem(item)"
          />
        </div>
      </div>

      <div class="flex-1 border rounded p-4">
        <h2 class="text-xl font-semibold mb-4">Список 2</h2>
        <div class="grid grid-cols-3 gap-2">
          <Item
              v-for="item in rightItems"
              :key="'available-' + item.id"
              :item="item"
              :selected="selectedRightItem?.id === item.id"
              @select="selectRightItem(item)"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import Item from './components/Item.vue'

interface IItem {
  id: number
  name: string
}

const leftItems = ref<IItem[]>([
  {
    "id": 1,
    "name": "Shoes 1"
  },
  {
    "id": 2,
    "name": "Shoes 2"
  },
  {
    "id": 3,
    "name": "Shoes 3"
  },
  {
    "id": 4,
    "name": "Shoes 4"
  },
  {
    "id": 5,
    "name": "T-shirt 1"
  },
  {
    "id": 6,
    "name": "T-shirt 2"
  },
  {
    "id": 7,
    "name": "T-shirt 3"
  },
  {
    "id": 8,
    "name": "T-shirt 4"
  }
])

const rightItems = ref<IItem[]>([
  {
    "id": 11,
    "name": "Jacket 1"
  },
  {
    "id": 12,
    "name": "Jacket 2"
  },
  {
    "id": 13,
    "name": "Jacket 3"
  },
  {
    "id": 14,
    "name": "Jacket 4"
  },
  {
    "id": 15,
    "name": "Hoodie 1"
  },
  {
    "id": 16,
    "name": "Hoodie 2"
  },
  {
    "id": 17,
    "name": "Hoodie 3"
  },
  {
    "id": 18,
    "name": "Hoodie 4"
  }
])

const selectedLeftItems = ref<IItem[]>([])
const selectedRightItem = ref<IItem | null>(null)

const selectLeftItem = (item: IItem) => {
  const index = selectedLeftItems.value.findIndex(i => i.id === item.id)

  if (index >= 0) {
    selectedLeftItems.value.splice(index, 1)
  } else if (selectedLeftItems.value.length < 4) {
    selectedLeftItems.value.push(item)
  }
}

const removeLeftItem = (index: number) => {
  selectedLeftItems.value.splice(index, 1)
}

const selectRightItem = (item: IItem) => {
  if (selectedRightItem.value?.id === item.id) {
    selectedRightItem.value = null
  } else {
    selectedRightItem.value = item
  }
}
</script>