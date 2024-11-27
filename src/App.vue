<template>
  <div>
    <button @click="showModal = true">Открыть</button>

    <Modal
      v-model="showModal"
      title="Выберите папку"
      @ok="handleOk"
    >
      <FolderTree
        :folders="folders"
        :selectedFolderId="selectedFolderId"
        @select="handleSelect"
      />
    </Modal>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import Modal from './components/ ModalElement.vue';
import FolderTree from './components/FolderTree.vue';
import { mockFolders } from './mock/folders';

const showModal = ref(false);
const selectedFolderId = ref<number>();
const folders = ref(mockFolders);

const handleSelect = (id: number) => {
  selectedFolderId.value = id;
};

const handleOk = () => {
  if (selectedFolderId.value) {
    console.log('Selected folder ID:', selectedFolderId.value);
  }
  showModal.value = false;
};
</script>
