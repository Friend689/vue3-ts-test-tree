<script setup lang="ts">
import { ref } from 'vue';

const emit = defineEmits(['close', 'confirm']);

defineProps({
  title: {
    type: String,
    required: true,
  },
});

const modalRef = ref<HTMLElement | null>(null);

// Function to handle clicks outside the modal
const handleClickOutside = (event: MouseEvent) => {
  if (modalRef.value && !modalRef.value.contains(event.target as Node)) {
    emit('close');
  }
};

</script>

<template>
  <div class="modal" @click="handleClickOutside">
    <div class="modal__container" ref="modalRef">
      <div class="modal__header">
        <h2>{{ title }}</h2>
      </div>
      <div class="modal__body">
        <slot></slot>
      </div>
      <div class="modal__footer">
        <button @click="emit('confirm')">Ок</button>
        <button @click="emit('close')">Закрыть</button>
      </div>
    </div>
  </div>
</template>

<style>
.modal {
  color: black;
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.02);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
}

.modal__container {
  width: 400px;
  height: 500px;
  background-color: #fff;
  border-radius: 8px;
  display: flex;
  flex-direction: column;
}

.modal__header {
  padding: 16px;
  border-bottom: 1px solid #ccc;
}

.modal__body {
  padding: 16px;
  max-height: 400px;
  overflow-y: auto;
  flex-grow: 1;
}

.modal__footer {
  padding: 16px;
  border-top: 1px solid #ccc;
  display: flex;
  justify-content: flex-end;
}

.modal__footer button {
  margin-left: 8px;
  padding: 8px 16px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.modal__footer button:hover {
  background-color: #f0f0f073;
}
</style>
