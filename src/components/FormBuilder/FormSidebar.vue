<template>
  <div class="form-sidebar">
    <div class="components-list">
      <div class="components-title">
        <svg-icon icon-class="component" />
        <!-- <el-icon><Notification /></el-icon> -->
        输入型组件
      </div>
      <draggable
        class="components-draggable"
        :list="inputComponents"
        :group="{ name: 'componentsGroup', pull: 'clone', put: false }"
        :clone="cloneComponent"
        draggable=".components-item"
        :sort="false"
        @end="onEnd"
      >
        <template #item="{ element }">
          <div class="draggable-item">
            <div class="components-item" @click="addComponent(element)">
              <div class="components-body">
                <svg-icon :icon-class="element.tagIcon" />
                {{ element.label }}
              </div>
            </div>
          </div>
        </template>
      </draggable>
    </div>
  </div>
</template>

<script setup>
import { inputComponents } from './config/index.js';
import draggable from 'vuedraggable';

const emit = defineEmits(['dragStart']);

const formTypes = [
  { type: 'input', preview: 'InputPreview' },
  { type: 'textarea', preview: 'TextareaPreview' },
  { type: 'select', preview: 'SelectPreview' },
  { type: 'checkbox', preview: 'CheckboxPreview' },
  { type: 'radio', preview: 'RadioPreview' }
];

const onDragStart = type => {
  emit('dragStart', type); // 触发拖拽开始事件，传递类型
};

const cloneComponent = () => {};

const addComponent = element => {
  console.log(element);
};

const onEnd = () => {};
</script>

<style lang="scss">
$selectedColor: #f6f7ff;
$lighterBlue: #409eff;

.form-sidebar {
  box-sizing: border-box;
  width: 220px;
  padding: 20px;
  background-color: #eaeaea;
  border-right: 1px solid #ddd;
}
.form-type {
  padding: 10px;
  margin-bottom: 10px;
  background: white;
  border-radius: 4px;
  cursor: grab;
  text-align: center;
}
.form-type:active {
  cursor: grabbing;
}
.form-preview {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 40px;
  font-size: 14px;
  color: #666;
  border: 1px dashed #ccc;
}

.components-list {
  padding: 8px;
  box-sizing: border-box;
  height: 100%;
  .components-item {
    display: inline-block;
    width: 48%;
    margin: 1%;
    transition: transform 0ms !important;
  }
}
.components-draggable {
  padding-bottom: 20px;
}
.components-title {
  font-size: 14px;
  color: #222;
  margin: 6px 2px;
  .svg-icon {
    color: #666;
    font-size: 18px;
  }
}

.components-body {
  padding: 8px 10px;
  background: $selectedColor;
  font-size: 12px;
  cursor: move;
  border: 1px dashed $selectedColor;
  border-radius: 3px;
  .svg-icon {
    color: #777;
    font-size: 15px;
  }
  &:hover {
    border: 1px dashed #787be8;
    color: #787be8;
    .svg-icon {
      color: #787be8;
    }
  }
}
</style>
