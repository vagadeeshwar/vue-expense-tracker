<template>
    <div>
        <h3>History</h3>
        <ul>
            <template v-for="({ id, text, amount }, index) in data" :key="id">
                <li class="list-item" :class="{ 'income': amount >= 0, 'expense': amount < 0 }">
                    <div class="x_btn" @click="emit('removeTransaction', index)">x</div>
                    {{ text }}
                    <span>{{ amount >= 0 ? '+' : '-' }}${{ Math.abs(amount) }}</span>
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
    background-color: red;
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

.income span {
    border-right: 2px solid green;
}

.expense span {
    border-right: 2px solid red;
}
</style>