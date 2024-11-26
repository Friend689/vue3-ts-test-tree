<script setup lang="ts">
import { ref } from "vue";
import Modal from "../components/ui/ModalComponent.vue";
import FolderTree from "../components/ui/FolderTreeComponent.vue";

const isModalOpen = ref(false);
const selectedFolderId = ref<number | null>(null);

const mockFolders = [
  {
    id: 1, name: 'Папка 1', children: [
      { id: 2, name: 'Папка 1.1', children: [] },
      {
        id: 3, name: 'Папка 1.2', children: [
          { id: 4, name: 'Папка 1.2.1', children: [] }
        ]
      }
    ]
  },
  { id: 5, name: 'Папка 2', children: [] },
];

const openModal = () => {
  isModalOpen.value = true;
};

const closeModal = () => {
  isModalOpen.value = false;
};

const confirmSelection = () => {
  // Здесь можно выполнить действия с выбранной папкой
  console.log('Выбранная папка: ', selectedFolderId.value);
  closeModal();
  // alert('Выбранная папка: ' + selectedFolderId.value);
};
</script>

<template>
  <div>
    <button @click="openModal">Открыть</button>
    <Modal v-if="isModalOpen" @close="closeModal" @confirm="confirmSelection" title="Выберите папку">
      <FolderTree :folders="mockFolders" v-model="selectedFolderId" />
    </Modal>
  </div>
</template>
