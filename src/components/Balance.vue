<template>
    <div>
        <h3>your balance</h3>
        <div>{{ balance >= 0 ? `+$${balance}` : `-$${-balance}` }}</div>
    </div>
</template>

<script setup>

const props = defineProps({
    balance: { type: Number, required: true }
})

</script>