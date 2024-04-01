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

defineProps({
    income: Number,
    expense: Number
})
</script>