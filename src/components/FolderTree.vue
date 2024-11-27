<template>
  <div class="folder-tree">
    <div
      v-for="folder in folders"
      :key="folder.id"
      class="folder-item"
      :style="{ marginLeft: '20px' }"
    >
      <div class="folder-row">
        <span
          v-if="folder.children.length"
          @click="toggleFolder(folder.id)"
          class="folder-toggle"
        >
        {{ expandedFolders.has(folder.id) ? '⏬' : '⏩' }}
        </span>
        <span
          class="folder-name"
          :class="{ 'selected': selectedFolderId === folder.id }"
          @click="selectFolder(folder.id)"
        >
          📁 {{ folder.name }}
        </span>
      </div>

      <FolderTree
        v-if="expandedFolders.has(folder.id)"
        :folders="folder.children"
        :selectedFolderId="selectedFolderId"
        @select="$emit('select', $event)"
      />
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import type { Folder } from '../types/folder.ts';

defineProps<{
  folders: Folder[];
  selectedFolderId?: number;
}>();

const emit = defineEmits<{
  (e: 'select', id: number): void;
}>();

const expandedFolders = ref(new Set<number>());

const toggleFolder = (id: number) => {
  if (expandedFolders.value.has(id)) {
    expandedFolders.value.delete(id);
  } else {
    expandedFolders.value.add(id);
  }
};

const selectFolder = (id: number) => {
  emit('select', id);
};
</script>

<style scoped>
.folder-item {
  padding: 4px 0;
}

.folder-row {
  display: flex;
  align-items: center;
  cursor: pointer;
}

.folder-toggle {
  margin-right: 8px;
  cursor: pointer;
}

.folder-name {
  padding: 2px 4px;
  color: #000000;
}

.selected {
  background-color: #e0e0e0;
  border-radius: 4px;
}
</style>
