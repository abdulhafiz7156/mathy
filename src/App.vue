<script setup>

import {onMounted, ref} from "vue";

const numbers = ref([]);
const count = ref(6);
const totalNumbers = ref([])
const result = ref(null)
const inputValue = ref(null)
const resultDisplay = ref(false)

const generateRandomNumbers = () => {
  const generatedNumbers = [];
  for (let i = 0; i < count.value; i++) {
    setTimeout(() => {
      generatedNumbers.pop(); // Remove the last number
      const newNumber = Math.floor(Math.random() * 10) + 1;
      generatedNumbers.push(newNumber); // Add a new random number
      numbers.value = [...generatedNumbers]; // Update numbers array
      totalNumbers.value.push(newNumber); // Push the new number to totalNumbers array
    }, i * 1000);
  }
  numbers.value = generatedNumbers;
};

const checkAnswer = () => {
  result.value = totalNumbers.value.reduce((acc, curr) => acc + curr, 0).toString();
  console.log(result.value)
  console.log(inputValue.value)
  if (inputValue.value === result.value) {
    resultDisplay.value = true;
  } else {

  }
}

onMounted(() => {
  generateRandomNumbers()
})
</script>

<template>
  <div>
    <ul>
      <li v-for="(number, index) in numbers" :key="index">{{ number }}</li>
    </ul>
    <input type="text" placeholder="Enter your result" v-model="inputValue">
    <p v-if="resultDisplay">Javob tog'ri {{result}}</p>
    <button @click="checkAnswer()">click on me</button>
  </div>
</template>

<style scoped>
li {
  list-style: none;
  font-size: 50px;

}
</style>
