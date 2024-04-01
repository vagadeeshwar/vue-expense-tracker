<template>
  <div>
    <Header />
    <Balance :balance="balance" />
    <IncomeExpenses :income="income" :expense="expense" />
    <TransactionList :data="data" />
    <AddTransaction @newTransaction="addTransaction" />
  </div>
</template>

<script setup>
import { defineAsyncComponent, ref } from 'vue';

const Header = defineAsyncComponent(() => import('./components/Header.vue'));
const Balance = defineAsyncComponent(() => import('./components/Balance.vue'));
const AddTransaction = defineAsyncComponent(() => import('./components/AddTransaction.vue'));
const IncomeExpenses = defineAsyncComponent(() => import('./components/IncomeExpenses.vue'));
const TransactionList = defineAsyncComponent(() => import('./components/TransactionList.vue'));

const data = ref([]), balance = ref(0), income = ref(0), expense = ref(0);

const addTransaction = (transaction) => {
  let amount = parseFloat(transaction.amount);
  data.value.push(transaction)
  balance.value += amount;
  if (amount >= 0) income.value += amount;
  else expense.value += amount;

}
</script>