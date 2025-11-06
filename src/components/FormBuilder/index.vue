<template>
  <div class="form-builder">
    <FormSidebar @dragStart="handleDragStart" />
    <FormCanvas
      :initialItems="formItems"
      :selectedItem="selectedItem"
      @updateItems="updateFormItems"
      @selectItem="selectItem"
    />
    <FormConfigPanel
      v-if="selectedItem"
      :selectedItem="selectedItem"
      @updateItem="updateSelectedItem"
    />
  </div>
</template>

<script setup>
import { ref } from 'vue';
import FormSidebar from './FormSidebar.vue';
import FormCanvas from './FormCanvas.vue';
import FormConfigPanel from './FormConfigPanel.vue';

const formItems = ref([]);
const selectedItem = ref(null);

const handleDragStart = type => {
  event.dataTransfer.setData('text/plain', JSON.stringify(type));
};

const updateFormItems = newItems => {
  formItems.value = newItems;
};

const selectItem = item => {
  selectedItem.value = item;
};

const updateSelectedItem = updatedItem => {
  const index = formItems.value.findIndex(item => item.id === updatedItem.id);
  if (index !== -1) {
    formItems.value[index] = { ...updatedItem };
  }
};
</script>

<style>
.form-builder {
  display: flex;
  height: 100vh;
}
</style>
