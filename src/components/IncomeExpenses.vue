<template>

    <div class="d-flex justify-content-between">
        <div class="text-center">
            <div class="fw-bold">Income</div>
            <div class="text-success">+${{ income }}</div>
        </div>
        <div class="text-center">
            <div class="fw-bold">Expense</div>
            <div class="text-danger">-${{ -expense }}</div>
        </div>
    </div>
</template>

<script setup>

const props = defineProps({
    income: { type: Number, required: true },
    expense: { type: Number, required: true }
})
</script>