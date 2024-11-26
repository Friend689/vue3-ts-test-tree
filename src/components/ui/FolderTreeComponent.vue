<script setup lang="ts">
import { ref } from "vue";
import FolderTree from "./FolderTreeComponent.vue";

type FolderItem = {
  id: number;
  name: string;
  children: FolderItem[];
}

const emit = defineEmits(['update:modelValue']);

const props = defineProps({
  folders: {
    type: Array as () => FolderItem[],
    required: true,
  },
  modelValue: {
    type: Number as () => number | null,
    default: null,
  },
});

const toggle = (folder: FolderItem) => {
  const newValue = props.modelValue === folder.id ? null : folder.id;
  emit('update:modelValue', newValue);
};

// Function to check if the folder is selected
const isSelected = (id: number) => {
  return props.modelValue === id;
};

const emitUpdate = (newValue: number | null) => {
  emit('update:modelValue', newValue);
};
</script>

<template>
  <ul>
    <li v-for="folder in folders" :key="folder.id">
      <div @click="toggle(folder)" :class="{ selected: isSelected(folder.id) }">
        {{ folder.name }}
      </div>
      <FolderTree v-if="folder.children.length" :folders="folder.children" :modelValue="modelValue"
        @update:modelValue="emitUpdate" />
    </li>
  </ul>
</template>

<style scoped>
.selected {
  font-weight: bold;
}

div {
  cursor: pointer;
}
</style>
