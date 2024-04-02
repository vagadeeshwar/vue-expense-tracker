<template>
  <div class="container">
    <Header />
    <Balance :balance />
    <IncomeExpenses :income :expense />
    <TransactionList :data @removeTransaction="removeTransaction" />
    <AddTransaction @newTransaction="addTransaction" :balance /> <button class="btn btn-danger mt-4"
      @click="clearStorage">Clear Local Storage</button>
  </div>
</template>

<script setup>

import { defineAsyncComponent, ref, watchEffect, onMounted } from 'vue';
const Header = defineAsyncComponent(() => import('./components/Header.vue'));
const Balance = defineAsyncComponent(() => import('./components/Balance.vue'));
const AddTransaction = defineAsyncComponent(() => import('./components/AddTransaction.vue'));
const IncomeExpenses = defineAsyncComponent(() => import('./components/IncomeExpenses.vue'));
const TransactionList = defineAsyncComponent(() => import('./components/TransactionList.vue'));
import 'vue-toast-notification/dist/theme-sugar.css';
import { useToast } from 'vue-toast-notification';

const data = ref([]), balance = ref(0), income = ref(0), expense = ref(0);
const instance = useToast()

watchEffect(() => {
  if (data.value.length > 0)
    localStorage.setItem('data', JSON.stringify({ data: data.value, balance: balance.value, income: income.value, expense: expense.value }));
})

onMounted(() => {
  const storedData = localStorage.getItem('data');
  if (storedData) {
    const parsedData = JSON.parse(storedData);
    data.value = parsedData.data || [];
    balance.value = parsedData.balance || 0;
    income.value = parsedData.income || 0;
    expense.value = parsedData.expense || 0;
  }
})

const addTransaction = (transaction) => {
  let amount = parseFloat(transaction.amount);
  data.value.push(transaction)
  balance.value += amount;
  if (amount >= 0) income.value += amount;
  else expense.value += amount;
}

const removeTransaction = (index) => {
  const amount = data.value[index].amount;

  if (amount >= 0 && income.value - amount < -expense.value) {
    instance.error("Income can't be lower than expense!", {
      position: "top-right"
    });
    instance.info("Try removing Expenses first!", {
      position: "top-right"
    });
  } else {
    balance.value -= amount;
    if (amount >= 0) {
      income.value -= amount;
    } else {
      expense.value -= amount;
    }
    data.value.splice(index, 1);
  }
};

const clearStorage = () => {
  localStorage.clear();
}
</script>

<style scoped>
.container {
  max-width: 400px;
  margin: 30px auto;
  padding: 32px;
  background-color: #fff;
  border-radius: 5px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  outline: 2px solid black;
  row-gap: 8px;
}
</style>