<template>
    <div>
        <h3>Add new Transaction</h3>
        <form action="" id="form">
            <label for="text">Text</label>
            <input type="text" placeholder="Enter text..." id="text" v-model="text" required>
            <label for="amount">Amount<div> (negative - expense, positive - income)</div></label>
            <input type="text" placeholder="Enter amount..." id="amount" v-model.number="amount" required>
            <button @click.prevent="addTransaction">Add Transaction</button>
        </form>
    </div>
</template>

<script setup>
import { ref } from 'vue'
import 'vue-toast-notification/dist/theme-sugar.css';
import { useToast } from 'vue-toast-notification';

const $toast = useToast();
const text = ref(""), amount = ref("")
const instance = $toast

const emit = defineEmits(['newTransaction'])

const addTransaction = () => {
    if (text.value === "" || amount.value === "") {
        instance.warning('Empty values not allowed!', {
            position: "top-right"
        });
    }
    else if (amount.value.strip() === "0") {
        instance.warning('Amount can"t be 0!', {
            position: "top-right"
        });
    }
    else {
        emit('newTransaction', { text: text.value, amount: amount.value })
        instance.success('Your expense  was succesfully added!', {
            position: "top-right"
        });


    }
    text.value = ""
    amount.value = ""
}
</script>