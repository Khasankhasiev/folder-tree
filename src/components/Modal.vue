<template>
    <div class="modal-overlay">
        <div class="modal-content">
            <h2 class="modal-title">{{ title }}</h2>
            <slot></slot>
            <div class="modal-footer">
                <button class="btn btn-cancel" @click="$emit('close')">
                    Закрыть
                </button>
                <button class="btn btn-ok" @click="$emit('ok')">Ок</button>
            </div>
        </div>
    </div>
</template>

<script setup lang="ts">
defineProps({
    title: {
        type: String,
        required: true,
    },
});

defineEmits(['close', 'ok']);
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
    background: white;
    padding: 2rem;
    border-radius: 8px;
    width: 400px;
    max-width: 90%;
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
}

.modal-title {
    margin: 0 0 1rem;
    font-size: 1.5rem;
}

.modal-footer {
    display: flex;
    justify-content: flex-end;
    gap: 1rem;
}

.btn {
    padding: 0.5rem 1rem;
    border: none;
    border-radius: 4px;
    cursor: pointer;
}

.btn-cancel {
    background: #f5f5f5;
}

.btn-cancel:hover {
    background: #e0e0e0;
}

.btn-ok {
    background: #4caf50;
    color: white;
}

.btn-ok:hover {
    background: #43a047;
}
</style>
