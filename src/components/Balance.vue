<template>

    <div class="my-4">
        <h3 class="text-uppercase mb-2">Your Balance</h3>
        <div class="fs-3" :class="{ 'text-success': balance >= 0, 'text-danger': balance < 0 }"> {{ balance >= 0 ?
            `+$${balance}` : `-$${-balance}` }} </div>
    </div>
</template>

<script setup>

const props = defineProps({
    balance: { type: Number, required: true }
})

</script>