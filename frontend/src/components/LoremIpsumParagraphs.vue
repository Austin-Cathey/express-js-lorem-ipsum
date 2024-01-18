<template>
  <div>
    <input
      v-model="numberOfParagraphs"
      type="number"
      placeholder="How many paragraphs?"
    /><br />
    <button @click="generateLoremIpsumParagraphs" type="submit">
      Generate Paragraphs
    </button>
    <div v-if="generatedParagraphs">
      <h2>Generated Lorem Ipsum Text:</h2>
      <p v-for="(paragraph, index) in generatedParagraphs" :key="index">
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

const numberOfParagraphs = ref("");
const generatedParagraphs = ref(null);
const errorMsg = ref(null);

const generateLoremIpsumParagraphs = () => {
  errorMsg.value = null;
  fetch("http://localhost:3000/lorem/:" + numberOfParagraphs.value)
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
    generatedParagraphs,
    generateLoremIpsumParagraphs,
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
