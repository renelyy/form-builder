<template>
  <div class="form-config" v-if="selectedItem">
    <h4>表单项配置</h4>
    <div class="config-group">
      <label>标签名：</label>
      <input v-model="selectedItem.label" type="text" />
    </div>
    <div class="config-group">
      <label>是否必填：</label>
      <input v-model="selectedItem.required" type="checkbox" />
    </div>
    <div
      class="config-group"
      v-if="['select', 'radio', 'checkbox'].includes(selectedItem.type)"
    >
      <label>选项：</label>
      <div v-for="(option, index) in selectedItem.options" :key="index">
        <input
          v-model="selectedItem.options[index]"
          type="text"
          placeholder="选项内容"
        />
        <button @click="removeOption(index)">删除</button>
      </div>
      <button @click="addOption">添加选项</button>
    </div>
  </div>
</template>

<script setup>
const emit = defineEmits(['dragStart']);
const props = defineProps({
  selectedItem: {
    type: Object,
    default: () => {}
  }
});
const addOption = () => {
  if (!props.selectedItem.options) props.selectedItem.options = [];
  props.selectedItem.options.push('');
  emit('updateItem', props.selectedItem);
};

const removeOption = index => {
  props.selectedItem.options.splice(index, 1);
  emit('updateItem', props.selectedItem);
};
</script>

<style>
.form-config {
  width: 300px;
  padding: 20px;
  background-color: #f7f7f7;
  border-left: 1px solid #ddd;
}
.config-group {
  margin-bottom: 20px;
}
label {
  display: inline-block;
  width: 80px;
}
input[type='text'] {
  padding: 5px;
  width: calc(100% - 90px);
  margin-left: 10px;
}
button {
  margin-top: 10px;
  cursor: pointer;
}
</style>
