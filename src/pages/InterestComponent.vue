<template>
  <div>
    <div>
      <label for="initial-amount">Monto inicial:</label>
      <input type="number" v-model="initialAmount" id="initial-amount">
    </div>
    <div>
      <label for="monthly-deposit">Depósito mensual:</label>
      <input type="number" v-model="monthlyDeposit" id="monthly-deposit">
    </div>
    <button @click="calculateInterest">Calcular</button>
    <h2>Interés acumulado: {{ interest.toFixed(2) }} Bs.</h2>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const initialAmount = ref(0)
const monthlyDeposit = ref(250)
const interest = ref(0)

const calculateInterest = () => {
  const monthlyInterestRate = 0.0125 // 1.25% mensual
  let totalAmount = initialAmount.value

  for (let i = 1; i <= 12; i++) {
    totalAmount += monthlyDeposit.value
    totalAmount += totalAmount * monthlyInterestRate
  }

  interest.value = totalAmount - (initialAmount.value + monthlyDeposit.value * 12)
}
</script>
