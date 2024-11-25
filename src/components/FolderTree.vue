<template>
    <ul class="folder-tree">
        <li v-for="folder in folders" :key="folder.id" class="folder-item">
            <div class="folder-content">
                <input
                    type="checkbox"
                    class="checkbox"
                    :checked="selectedIds.has(folder.id)"
                    @change="toggleSelection(folder.id)"
                />
                <span @click="toggle(folder)" class="folder-name">
                    {{ folder.name }}
                </span>
                <button
                    v-if="folder.children.length"
                    class="toggle-btn"
                    @click.stop="toggle(folder)"
                >
                    {{ openedIds.has(folder.id) ? '-' : '+' }}
                </button>
            </div>
            <FolderTree
                v-if="openedIds.has(folder.id) && folder.children.length"
                :folders="folder.children"
                :selected-ids="selectedIds"
                @update:selected-ids="updateSelectedIds"
            />
        </li>
    </ul>
</template>

<script setup lang="ts">
import { ref, defineProps, defineEmits } from 'vue';

const props = defineProps({
    folders: {
        type: Array as () => { id: number; name: string; children: any[] }[],
        required: true,
    },
    selectedIds: {
        type: Set as () => Set<number>,
        required: true,
    },
});

const emit = defineEmits(['update:selected-ids']);
const openedIds = ref(new Set<number>());

const toggle = (folder: { id: number }) => {
    if (openedIds.value.has(folder.id)) {
        openedIds.value.delete(folder.id);
    } else {
        openedIds.value.add(folder.id);
    }
};

const toggleSelection = (id: number) => {
    const newSelectedIds = new Set(props.selectedIds);
    if (newSelectedIds.has(id)) {
        newSelectedIds.delete(id);
    } else {
        newSelectedIds.add(id);
    }
    emit('update:selected-ids', newSelectedIds);
};

const updateSelectedIds = (newSelectedIds: Set<number>) => {
    emit('update:selected-ids', newSelectedIds);
};
</script>

<style scoped>
.folder-tree {
    list-style: none;
    padding-left: 1rem;
}

.folder-item {
    margin-bottom: 0.5rem;
}

.folder-content {
    display: flex;
    align-items: center;
    gap: 0.5rem;
}

.checkbox {
    accent-color: #4caf50;
}

.folder-name {
    cursor: pointer;
    font-weight: bold;
}

.toggle-btn {
    background: none;
    border: none;
    font-size: 1rem;
    cursor: pointer;
}

.toggle-btn:hover {
    color: #007bff;
}
</style>
