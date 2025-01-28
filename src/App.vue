<script setup>
import Header from "./components/Header.vue";
import Balance from "./components/Balance.vue";
import IncomeExp from "./components/IncomeExp.vue";
import TransacList from "./components/TransacList.vue";
import AddTrans from "./components/AddTrans.vue";
import { ref, computed, onMounted } from "vue";

import { useToast } from "vue-toastification";

const toast = useToast();

onMounted(() => {
  const savedTransac = JSON.parse(localStorage.getItem("transactions"));

  if (savedTransac) {
    transactions.value = savedTransac;
  }
});

const transactions = ref([]);
// get total
const total = computed(() => {
  return transactions.value.reduce((acc, transaction) => {
    return acc + transaction.amount;
  }, 0);
});

// get income
const income = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount > 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0)
    .toFixed(2);
});

// get expense
const expenses = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount < 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0)
    .toFixed(2);
});

// handler

const handleTransac = (transactionData) => {
  transactions.value.push({
    id: genereateId(),
    text: transactionData.text,
    amount: transactionData.amount,
  });
  saveToLocalStorage();
  toast.success("Transaction added");
};

//generate id
const genereateId = () => {
  return Math.floor(Math.random() * 100000000);
};

// delete transaction

const handleDeleted = (id) => {
  transactions.value = transactions.value.filter(
    (transaction) => transaction.id !== id
  );
  saveToLocalStorage();

  toast.error("Transaction deleted");
};

//save to local storage
const saveToLocalStorage = () => {
  localStorage.setItem("transactions", JSON.stringify(transactions.value));
};
</script>

<template>
  <Header />
  <div class="container">
    <Balance :total="+total" />
    <IncomeExp :income="+income" :expenses="+expenses" />
    <TransacList :transactions="transactions" @deleteTransac="handleDeleted" />
    <AddTrans @transacSubmit="handleTransac" />
  </div>
</template>

<style scoped>
.container {
  box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px;
  padding: 20px;
}
</style>
