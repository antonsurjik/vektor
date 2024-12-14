<template>
  <article class="container">
    <input
      type="text"
      v-model="text"
      :maxlength="maxLength"
      class="input"
      placeholder="Введите текст"
    />
    <p class="counter" :style="{ color: textColor }">
      Осталось символов: {{ letters_ostalos }}
    </p>
  </article>
</template>

<script setup>
import { computed, ref } from "vue";
let maxLength = 50;
let text = ref("");
let letters_ostalos = computed(() => maxLength - text.value.length);

let textColor = computed(() => {
  if (letters_ostalos.value >= 25) return "black";
  if (letters_ostalos.value >= 15) return "yellow";
  if (letters_ostalos.value >= 10) return "orange";
  if (letters_ostalos.value >= 1) return "red";
  return "maroon";
});
</script>

<style>
.container {
  font-family: Arial, sans-serif;
  text-align: center;
  margin: 50px auto;
  max-width: 400px;
}

.input {
  width: 100%;
  padding: 10px;
  font-size: 16px;
  border: 1px solid #ddd;
  border-radius: 5px;
  margin-bottom: 20px;
}

.counter {
  font-size: 18px;
  font-weight: bold;
  margin-top: 10px;
}
</style>