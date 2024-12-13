<template>
  <div class="inventory-page container">
    <div class="inventory-page__block-wrap">
      <InventoryBlock
        title="Выбранные вещи пользователя"
        :items="selectedUserItems"
        :removable="true"
        @itemAdd="addUserItem"
        @itemRemove="removeUserItem"
      >
        <template #count>
          <div class="inventory-page__selected-count">Выбрано: {{ selectedUserItems.length }} / 6</div>
        </template>
      </InventoryBlock>
      <InventoryBlock
        title="Выбранная вещь на выбор"
        :items="selectedChoiceItem"
        :removable="false"
        @itemAdd="addChoiceItem"
      />
    </div>
    <div class="inventory-page__block-wrap">
      <InventoryBlock
        title="Вещи у пользователя"
        :items="userItems"
        :removable="false"
        @itemAdd="addUserItem"
      />
      <InventoryBlock
        title="Вещи на выбор"
        :items="choiceItems"
        :removable="false"
        @itemAdd="addChoiceItem"
      />
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import InventoryBlock from '../components/InventoryBlock.vue'

interface Item {
  id: number
  name: string
}

const userItems = ref<Item[]>([
  { id: 1, name: 'Shoes 1' },
  { id: 2, name: 'Shoes 2' },
  { id: 3, name: 'Shoes 3' },
  { id: 4, name: 'Shoes 4' },
  { id: 5, name: 'T-shirt 1' },
  { id: 6, name: 'T-shirt 2' },
  { id: 7, name: 'T-shirt 3' },
  { id: 8, name: 'T-shirt 4' },
])

const choiceItems = ref<Item[]>([
  { id: 11, name: 'Jacket 1' },
  { id: 12, name: 'Jacket 2' },
  { id: 13, name: 'Jacket 3' },
  { id: 14, name: 'Jacket 4' },
  { id: 15, name: 'Hoodie 1' },
  { id: 16, name: 'Hoodie 2' },
  { id: 17, name: 'Hoodie 3' },
  { id: 18, name: 'Hoodie 4' },
])

const selectedUserItems = ref<Item[]>([])
const selectedChoiceItem = ref<Item[]>([])

const addUserItem = (item: Item) => {
  if (selectedUserItems.value.length < 6 && !selectedUserItems.value.includes(item)) {
    selectedUserItems.value.push(item)
  }
}

const removeUserItem = (item: Item) => {
  const index = selectedUserItems.value.indexOf(item)
  if (index !== -1) {
    selectedUserItems.value.splice(index, 1)
  }
}

const addChoiceItem = (item: Item) => {
  selectedChoiceItem.value = [item]
}
</script>

<style lang="scss" scoped>
.inventory-page {
  &__block-wrap {
    display: flex;
    justify-content: space-between;
    margin: 0 auto;
    &:not(:last-child) {
      margin-bottom: 2rem;
    }
  }
  &__selected-count {
    text-align: center;
    font-size: 1rem;
    font-weight: 600;
    margin-top: 1rem;
  }
}
</style>
