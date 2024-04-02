<template>

    <div>
        <h3>Add new Transaction</h3>
        <form action="" id="form">
            <div class="mb-3"> <label for="text" class="form-label">Text</label> <input type="text" class="form-control"
                    placeholder="Enter text..." id="text" v-model.trim="text" required> </div>
            <div class="mb-3"> <label for="amount" class="form-label">Amount <div class="form-text">(negative - expense,
                        positive - income)</div> </label> <input type="text" class="form-control"
                    placeholder="Enter amount..." id="amount" v-model.number="amount" required> </div> <button
                class="btn btn-primary" @click.prevent="addTransaction">Add Transaction</button>
        </form>
    </div>
</template>

<script setup>
import { ref } from 'vue'
import 'vue-toast-notification/dist/theme-sugar.css';
import { useToast } from 'vue-toast-notification';
import { v4 as uuidv4 } from 'uuid';

const text = ref(""), amount = ref("")
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
        emit('newTransaction', { id: uuidv4(), text: text.value, amount: amount.value })
        instance.success(`Your ${amount.value >= 0 ? "income of +$" : "expense of -$"}${Math.abs(amount.value)} was succesfully added!`, {
            position: "top-right"
        });


    }
    text.value = ""
    amount.value = ""
}
</script>
<style scoped>
h3 {
    text-transform: uppercase;
    margin-top: 8px;
    font-size: medium;
    font-weight: 600;
}
</style>