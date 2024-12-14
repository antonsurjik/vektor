<template>
  <article class="rating-container">
    <article class="background-image">
      <article class="stars">
        <span
          v-for="n in totalStars"
          class="star"
          :class="{ active: n <= selectedStars }"
          @click="setRating(n)"
        >
          ★
        </span>
      </article>
    </article>
  </article>
</template>

<script setup>
import { ref } from "vue";

let totalStars = 5;

let selectedStars = ref(0);

function setRating(n) {
  selectedStars.value = n;
  alert(`Вы поставили ${n} звезд!`);
}
</script>

<style>
body {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: Arial, sans-serif;
}

.rating-container {
  position: relative;
  width: 100vw;
  height: 100vh;
  display: flex;
  align-items: flex-end;
  justify-content: center;
  background-color: #f5f5f5;
  overflow: hidden;
}

.background-image {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-image: url("https://i.pinimg.com/originals/2d/96/a9/2d96a9e420ae6dd9cbdeca0931dad1dd.jpg");
  background-size: cover;
  background-position: center;
  z-index: 1;
}

.stars {
  position: relative;
  z-index: 2;
  display: flex;
  justify-content: center;
  gap: 10px;
  margin-bottom: 50px;
}

.star {
  font-size: 50px;
  color: #ccc;
  cursor: pointer;
  transition: color 0.3s;
}

.star.active {
  color: #f39c12;
}

.star:hover {
  color: #f1c40f;
}
</style>