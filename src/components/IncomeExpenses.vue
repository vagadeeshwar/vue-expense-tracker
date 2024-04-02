<template>
    <div>
        <div>
            <div>Income</div>
            <div style="color:green">+${{ income }}</div>
        </div>
        <div>
            <div>Expense</div>
            <div style="color: red;">-${{ -expense }}</div>
        </div>
    </div>
</template>

<script setup>

const props = defineProps({
    income: { type: Number, required: true },
    expense: { type: Number, required: true }
})
</script>