<template>
  <div v-if="modelValue" class="modal-overlay">
    <div class="modal-content">
      <div class="modal-header">
        <h3>{{ title }}</h3>
      </div>

      <div class="modal-body">
        <slot></slot>
      </div>

      <div class="modal-footer">
        <button @click="$emit('ok')">Ок</button>
        <button @click="$emit('update:modelValue', false)">Закрыть</button>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
defineProps<{
  modelValue: boolean;
  title: string;
}>();

defineEmits<{
  (e: 'update:modelValue', value: boolean): void;
  (e: 'ok'): void;
}>();
</script>

<style scoped>
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal-content {
  background-color: white;
  padding: 20px;
  border-radius: 8px;
  min-width: 300px;
}

.modal-header {
  margin-bottom: 20px;
  color: #000000;
}

.modal-footer {
  margin-top: 20px;
  display: flex;
  justify-content: flex-end;
  gap: 10px;
}
</style>
