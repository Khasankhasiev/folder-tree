<template>
    <div class="app">
        <button class="open-modal-btn" @click="isModalOpen = true">
            Открыть
        </button>
        <Modal
            v-if="isModalOpen"
            title="Выберите папки"
            @close="isModalOpen = false"
            @ok="handleOk"
        >
            <FolderTree
                :folders="folders"
                :selected-ids="selectedIds"
                @update:selected-ids="setSelectedFolders"
            />
        </Modal>
    </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import Modal from './components/Modal.vue';
import FolderTree from './components/FolderTree.vue';
import { mockFolders } from './mockFolders';

const isModalOpen = ref(false);
const selectedIds = ref(new Set<number>());
const folders = ref(mockFolders);

const setSelectedFolders = (newSelectedIds: Set<number>) => {
    selectedIds.value = newSelectedIds;
};

const handleOk = () => {
    console.log('Выбранные ID папок:', Array.from(selectedIds.value));
    isModalOpen.value = false;
};
</script>

<style scoped>
.app {
    padding: 2rem;
}

.open-modal-btn {
    padding: 0.5rem 1rem;
    font-size: 1rem;
    background-color: #007bff;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
}

.open-modal-btn:hover {
    background-color: #0056b3;
}
</style>
