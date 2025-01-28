<template>
  <div class="inc-exp-container">
    <div>
      <h4>Pendapatan</h4>
      <p id="money-plus" class="money plus">+RP.{{ income }}k</p>
    </div>
    <div>
      <h4>Pengeluaran</h4>
      <p id="money-minus" class="money minus">RP.{{ expenses }}k</p>
    </div>
  </div>
</template>

<script setup>
import { defineProps } from "vue";

const props = defineProps({
  income: {
    type: Number,
    required: true,
  },
  expenses: {
    type: Number,
    required: true,
  },
});
</script>

<style></style>
