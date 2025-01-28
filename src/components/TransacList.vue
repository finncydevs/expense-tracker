<script setup>
import { defineProps } from "vue";
const emit = defineEmits(["deleteTransac"]);

const props = defineProps({
  transactions: {
    type: Array,
    required: true,
  },
});

const deleteTransac = (id) => {
  emit("deleteTransac", id);
};
</script>

<template>
  <div>
    <h3>Riwayat</h3>
    <ul id="list" class="list">
      <li
        v-for="transaction in transactions"
        :key="transaction.id"
        :class="transaction.amount < 0 ? 'minus' : 'plus'"
      >
        {{ transaction.text }} <span>${{ transaction.amount }}</span
        ><button class="delete-btn" @click="deleteTransac(transaction.id)">
          x
        </button>
      </li>
      <!-- <li class="minus">
        Cash <span>-$400</span><button class="delete-btn">x</button>
      </li>
      <li class="plus">
        paycheck <span>$400</span><button class="delete-btn">x</button>
      </li> -->
    </ul>
  </div>
</template>

<style></style>
