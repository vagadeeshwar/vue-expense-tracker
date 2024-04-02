<template>
    <div class="c">
        <h3>History</h3>
        <ul class="list-unstyled"> <template v-for="({ id, text, amount }, index) in data" :key="id">
                <li class="list-item"
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
h3 {
    margin-bottom: 0;
    border-bottom: 1px solid rgba(0, 0, 0, 0.3);
    padding-bottom: 4px;
    font-size: 1.3rem;
}

.c {
    padding-top: 16px;
}


.list-item {
    position: relative;
    list-style-type: none;
    margin-top: 10px;
    font-weight: 450;
    font-size: 0.9rem;
    display: flex;
    justify-content: space-between;
    padding: 0 4px;
}

.x_btn {
    position: absolute;
    left: -18px;
    /* width: 14px; */
    /* height: 14px; */
    bottom: -0.025px;
    color: rgb(0, 0, 0);
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