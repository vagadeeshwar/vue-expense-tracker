<template>
    <div>
        <h3>History</h3>
        <ul>
            <template v-for="(item, index) in data" :key="index">
                <li v-if="item.amount >= 0" style="border-right: 2px solid green;">
                    {{ item.text }} <span style="border-right: 2px solid green;">+${{ item.amount }}</span>
                </li>
                <li v-else>
                    {{ item.text }} <span style="border-right: 2px solid red;">-${{ -item.amount }}</span>
                </li>
            </template>
        </ul>
    </div>
</template>

<script setup>
defineProps({
    data: Array
})
</script>