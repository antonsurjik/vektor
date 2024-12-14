<template>
  <div class="posts">
    <h1>Список постов</h1>

    <div v-for="(post, index) in posts" class="post">
      <h2>{{ post.title }}</h2>
      <p>{{ post.content }}</p>

      <div class="controls">
        <button @click="dislikePost(index)" class="dislike">-</button>
        <span :class="{ negative: post.likes < 0 }">{{ post.likes }}</span>
        <button @click="likePost(index)" class="like">+</button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

let posts = ref([
  { id: 1, title: "Пост 1", content: "Содержание поста 1", likes: 0 },
  { id: 2, title: "Пост 2", content: "Содержание поста 2", likes: 0 },
  { id: 3, title: "Пост 3", content: "Содержание поста 3", likes: 0 },
]);

function likePost(index) {
  posts.value[index].likes++;
}

function dislikePost(index) {
  posts.value[index].likes--;
}
</script>

<style>
.posts {
  font-family: Arial, sans-serif;
  padding: 20px;
  max-width: 600px;
  margin: 0 auto;
}

.post {
  margin-bottom: 20px;
  padding: 15px;
  border: 1px solid #ddd;
  border-radius: 5px;
  background-color: #f9f9f9;
}

.post h2 {
  margin: 0 0 10px;
}

.controls {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 10px;
  gap: 10px;
}

button {
  padding: 10px 15px;
  font-size: 16px;
  font-weight: bold;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s;
}

button.like {
  background-color: #28a745;
  color: white;
}

button.dislike {
  background-color: #dc3545;
  color: white;
}

button:hover {
  opacity: 0.9;
}

span {
  font-size: 18px;
  font-weight: bold;
  min-width: 40px;
  text-align: center;
}

span.negative {
  color: #dc3545;
}
</style>