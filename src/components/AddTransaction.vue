<template>
    <div>
        <h3>Add new Transaction</h3>
        <form action="" id="form">
            <label for="text">Text</label>
            <input type="text" placeholder="Enter text..." id="text" v-model.trim="text" required>
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

const text = ref(""), amount = ref(""), id = ref(0)
const instance = useToast()
const emit = defineEmits(['newTransaction'])

const props = defineProps({
    balance: {
        type: Number,
        required: true
    }
})

const addTransaction = () => {
    if (text.value === "" || amount.value === "") {
        instance.warning('Empty values not allowed!', {
            position: "top-right"
        });
    }
    else if (isNaN(amount.value)) {
        instance.error('Amount has to be a number!', {
            position: "top-right"
        });
    }
    else if (amount.value === 0) {
        instance.warning("Amount can't be 0!", {
            position: "top-right"
        });
    }
    else if (amount.value < 0 && -amount.value > props.balance) {
        instance.error("The expense can't be more than the balance!", {
            position: "top-right"
        });
    }
    else {
        emit('newTransaction', { id: id.value++, text: text.value, amount: amount.value })
        instance.success('Your expense  was succesfully added!', {
            position: "top-right"
        });


    }
    text.value = ""
    amount.value = ""
}
</script>