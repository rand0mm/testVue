<template>
  <div class="inventory-block">
    <h2 class="inventory-block__caption">{{ title }}</h2>
    <transition-group
      name="fade"
      tag="ul"
      class="inventory-block__list"
    >
      <li
        v-for="item in items"
        :key="item?.id"
        class="inventory-block__item"
        @click="handleClick(item)"
      >
        {{ item?.name }}
      </li>
    </transition-group>
    <slot name="count"></slot>
  </div>
</template>

<script setup lang="ts">
import { defineProps, defineEmits } from 'vue'

interface Item {
  id: number
  name: string
}

const props = defineProps<{
  title: string
  items: Item[]
  removable: boolean
}>()

const emit = defineEmits<{
  (e: 'itemAdd', item: Item): void
  (e: 'itemRemove', item: Item): void
}>()

const handleClick = (item: Item) => {
  if (props.removable) {
    emit('itemRemove', item)
  } else {
    emit('itemAdd', item)
  }
}
</script>

<style lang="scss" scoped>
.inventory-block {
  width: 45%;
  border: 1px solid #ccc;
  padding: 1rem;
  border-radius: 0.5rem;

  box-sizing: border-box;
  &__caption {
    font-size: 1rem;
    font-weight: 600;
    text-align: center;
    margin-bottom: 1rem;
  }
  &__list {
    list-style: none;
    padding: 0;

    display: flex;
    flex-wrap: wrap;
    gap: 1rem;
    width: 100%;
  }
  &__item {
    cursor: pointer;
    padding: 1rem;
    text-align: center;
    border: 1px solid #ccc;
    border-radius: 0.25rem;
    &:hover {
      background-color: #f0f0f0;
    }
  }
}

.fade-enter-active,
.fade-leave-active {
  transition: all 0.5s;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
  transform: translateY(30px);
}
</style>
