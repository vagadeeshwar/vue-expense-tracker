<template>
    <div>
        <h3>your balance</h3>
        <div>{{ balance >= 0 ? `+$${balance}` : `-$${-balance}` }}</div>
    </div>
</template>

<script setup>

defineProps({
    balance: Number
})

</script>