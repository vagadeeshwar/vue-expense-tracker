<template>
    <div>
        <h3 class="mb-3">History</h3>
        <ul class="list-unstyled"> <template v-for="({ id, text, amount }, index) in data" :key="id">
                <li class="list-item py-2"
                    :class="{ 'border-end border-success border-3': amount >= 0, 'border-end border-danger border-3': amount < 0 }">
                    <div class="x_btn" @click="emit('removeTransaction', index)"> <i class="fas fa-times"></i> </div>
                    <span class="me-2">{{ text }}</span> <span>{{ amount >= 0 ? '+' : '-' }}${{ Math.abs(amount)
                        }}</span>
                </li>
            </template>
        </ul>
    </div>
</template>

<script setup>
const emit = defineEmits(['removeTransaction'])

const props = defineProps({
    data: {
        type: Array,
        required: true
    }
});
</script>

<style scoped>
.list-item {
    position: relative;
    list-style-type: none;
}

.x_btn {
    position: absolute;
    left: -20px;
    width: 16px;
    height: 16px;
    background-color: #dc3545;
    color: white;
    display: flex;
    justify-content: center;
    align-items: center;
    opacity: 0;
    transition: opacity 0.3s ease;
    cursor: pointer;
}

.list-item:hover .x_btn {
    opacity: 1;
}
</style>