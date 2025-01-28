<template>
  <h3>Tambahkan Transaksi Baru</h3>
  <form id="form" @submit.prevent="onSubmit">
    <div class="form-control">
      <label for="text">Text</label>
      <input
        type="text"
        id="text"
        placeholder="Masukan teks..."
        v-model="text"
      />
    </div>
    <div class="form-control">
      <label for="amount"
        >Jumlah <br />
        (minus - Pengeluaran, positive - Pendapatan)</label
      >
      <input
        type="text"
        id="amount"
        placeholder="Enter amount..."
        v-model="amount"
      />
    </div>
    <button class="btn">Tambahkan Transaksi</button>
  </form>
</template>

<script setup>
import { ref } from "vue";
import { useToast } from "vue-toastification";

const emit = defineEmits(["transacSubmit"]);
const toast = useToast();

const text = ref("");
const amount = ref("");

const onSubmit = () => {
  if (!text.value || !amount.value) {
    toast.error("Please add a text and amount");
    return;
  }

  const transactionData = {
    text: text.value,
    amount: parseFloat(amount.value),
  };

  emit("transacSubmit", transactionData);

  text.value = "";
  amount.value = "";
};
</script>

<style></style>
