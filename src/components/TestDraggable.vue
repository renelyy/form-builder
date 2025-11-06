<template>
  <draggable
    v-model="myArray"
    group="people"
    @start="onStart"
    @end="onEnd"
    item-key="id"
  >
    <template #item="{ element }">
      <div class="draggable-item">
        {{ element.name }}
      </div>
    </template>
  </draggable>
</template>

<script setup>
import { ref } from 'vue';
import draggable from 'vuedraggable';

const drag = ref(false);

const myArray = ref([
  { id: 1, name: 'Alice' },
  { id: 2, name: 'Bob' },
  { id: 3, name: 'Charlie' }
]);

const onStart = params => {
  console.log('Drag started', params);
  drag.value = true;
};

const onEnd = params => {
  console.log('Drag ended', params);
  drag.value = false;
};
</script>

<style lang="scss" scoped>
.draggable-item {
  border: 1px solid #ccc;
  padding: 10px;
  margin: 10px 0;
  background-color: #f9f9f9;
  border-radius: 5px;
  width: 200px;
  text-align: center;
}
</style>
