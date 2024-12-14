<template>
  <article class="container">
    <article class="controls">
      <input
        type="range"
        v-model="width"
        min="50"
        max="500"
        class="slider"
      />
      <input
        type="range"
        v-model="height"
        min="50"
        max="500"
        class="slider"
      />
    </article>

    <article class="square" :style="{width: `${width}px`, height: `${height}px`}"></article>
  </article>
</template>

<script setup>
import { ref } from "vue";

let width = ref(200);
let height = ref(200);
</script>

<style>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
  font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
}

.controls {
  position: absolute;
  top: 0;
  display: flex;
  flex-direction: row;
  gap: 50px;
}

.slider {
  width: 200px;
  margin: 20px auto;
  -webkit-appearance: none;
  background: #ddd;
  border-radius: 5px;
  height: 8px;
  outline: none;
}

.square {
  background-color: #7c9e00;
  transition: all 0.3s ease;
}
</style>