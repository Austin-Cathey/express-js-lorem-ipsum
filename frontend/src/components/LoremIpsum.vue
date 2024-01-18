<template>
  <div id="app">
    <h1>Lorem Ipsum Generator</h1>
    <button @click="generateLoremIpsum" type="submit">Generate</button>
    <div v-if="generatedText">
      <h2>Generated Lorem Ipsum Text:</h2>
      <p v-for="(paragraph, index) in generatedText" :key="index">
        {{ paragraph }}
      </p>
    </div>
    <div v-if="errorMsg" class="error">
      <p>{{ errorMsg }}. Please try again.</p>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const generatedText = ref(null);
const errorMsg = ref(null);

const generateLoremIpsum = () => {
  errorMsg.value = null;
  fetch("http://localhost:3000/lorem")
    .then((response) => response.json())
    .then((data) => {
      generatedText.value = data;
      console.log(generatedText);
    })
    .catch((error) => {
      errorMsg.value = error.message;
      console.error(error);
    });
  return {
    generatedText,
    generateLoremIpsum,
    errorMsg,
  };
};
</script>

<style scoped>
.error {
  background-color: #fbacbe;
  padding: 0.5rem;
  margin-top: 1rem;
}
</style>
