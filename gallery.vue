<template>
  <article class="gallery">
    <h1>Галерея изображений</h1>

    <article class="image-container">
      <img :src="images[this_index]" alt="Галерея изображений" />
    </article>

    <article class="controls">
      <button @click="prev_img" :disabled="this_index === 0">Назад</button>
      <button @click="next_img" :disabled="this_index === images.length - 1">Вперед</button>
    </article>
  </article>
</template>

<script setup>
import { ref } from "vue";

let this_index = ref(0);
let images = ref([
  "https://via.placeholder.com/600x400?text=Изображение+1",
  "https://via.placeholder.com/600x400?text=Изображение+2",
  "https://via.placeholder.com/600x400?text=Изображение+3",
  "https://via.placeholder.com/600x400?text=Изображение+4",
]);


function prev_img() {
  if (this_index.value > 0) {
    this_index.value--;
  }
}

function next_img() {
  if (this_index.value < images.value.length - 1) {
    this_index.value++;
  }
}
</script>

<style>
.gallery {
  font-family: Arial, sans-serif;
  text-align: center;
  padding: 20px;
}

.image-container {
  margin: 20px auto;
  max-width: 600px;
}

.image-container img {
  width: 100%;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}

.controls {
  display: flex;
  justify-content: center;
  gap: 10px;
  margin-top: 20px;
}

button {
  padding: 10px 20px;
  font-size: 16px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  background-color: #007bff;
  color: white;
  transition: background-color 0.3s;
}

button:disabled {
  background-color: #cccccc;
  cursor: not-allowed;
}

button:hover:not(:disabled) {
  background-color: #0056b3;
}
</style>