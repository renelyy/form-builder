<template>
  <div class="form-canvas" @dragover.prevent @drop="onDrop">
    <div
      v-for="(item, index) in formItems"
      :key="item.id"
      class="form-item"
      :class="{ selected: selectedItem?.id === item.id }"
      @click="selectItem(item)"
    >
      <component :is="item.type" class="form-item-preview" />
    </div>

    <TestDraggable />
  </div>
</template>

<script setup>
import { ref } from 'vue';
import TestDraggable from '../TestDraggable.vue';

const emit = defineEmits(['updateItems', 'selectItem']);
const props = defineProps({
  initialItems: {
    type: Array,
    default: () => []
  },
  selectedItem: {
    type: Object,
    default: () => {}
  }
});

const formItems = ref([...props.initialItems]);

const onDrop = event => {
  console.log(event.dataTransfer.getData('text/plain'))
  return;
  const draggedData = JSON.parse(event.dataTransfer.getData('text/plain'));
  const newItem = {
    id: Date.now(),
    type: draggedData.preview,
    label: '新表单项',
    required: false,
    options:
      draggedData.type === 'select' ||
      draggedData.type === 'radio' ||
      draggedData.type === 'checkbox'
        ? []
        : null
  };

  formItems.value.push(newItem);
  emit('updateItems', formItems.value);
};

const selectItem = item => {
  emit('selectItem', item);
};
</script>

<style>
.form-canvas {
  box-sizing: border-box;
  flex: 1;
  padding: 20px;
  background-color: #f9f9f9;
  min-height: 100%;
  border: 1px solid #ddd;
}
.form-item {
  margin-bottom: 10px;
  padding: 10px;
  background: white;
  border-radius: 4px;
  cursor: pointer;
}
.form-item.selected {
  border: 2px solid #0254a8;
}
.form-item-preview {
  padding: 10px;
  border: 1px solid #ccc;
}
</style>
