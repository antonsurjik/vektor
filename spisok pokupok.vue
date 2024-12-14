<template>
  <article class="shopping-list">
    <h1>Список покупок</h1>

    <form @submit.prevent="addItem">
      <input
        v-model="newItem"
        type="text"
        placeholder="Добавьте новый элемент"
        class="input"
      />
      <button type="submit" :disabled="!newItem.trim()">Добавить</button>
    </form>

    <ul>
      <li v-for="(item, index) in items" :key="index" class="list-item">
        <span v-if="!item.isEditing">{{ item.name }}</span>
        <input
          v-else
          v-model="item.name"
          @keyup.enter="finishEditing(item)"
          @blur="finishEditing(item)"
        />

        <article class="actions">
          <button @click="editItem(item)" v-if="!item.isEditing">✏️</button>
          <button @click="deleteItem(index)">🗑️</button>
        </article>
      </li>
    </ul>
  </article>
</template>

<script setup>
import { ref } from "vue";

let items = ref([]);
let newItem = ref("");

function addItem() {
  if (newItem.value.trim()) {
    items.value.push({ name: newItem.value.trim(), isEditing: false });
    newItem.value = "";
  }
}

function deleteItem(index) {
  items.value.splice(index, 1);
}

function editItem(item) {
  item.isEditing = true;
}

function finishEditing(item) {
  item.isEditing = false;
}
</script>

<style>
.shopping-list {
  font-family: Arial, sans-serif;
  padding: 20px;
  max-width: 400px;
  margin: 0 auto;
  text-align: center;
}

form {
  margin-bottom: 20px;
}

.input {
  padding: 10px;
  font-size: 16px;
  width: 70%;
  margin-right: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
}

button {
  padding: 10px 15px;
  font-size: 16px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s;
}

button[type="submit"] {
  background-color: #28a745;
  color: white;
}

button[type="submit"]:disabled {
  background-color: #cccccc;
  cursor: not-allowed;
}

ul {
  list-style: none;
  padding: 0;
}

.list-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
  margin-bottom: 10px;
  background-color: #f9f9f9;
}

.list-item input {
  flex: 1;
  margin-right: 10px;
  padding: 5px;
  border: 1px solid #ddd;
  border-radius: 5px;
}

.actions {
  display: flex;
  gap: 10px;
}

.actions button {
  background-color: transparent;
  font-size: 16px;
  cursor: pointer;
}
</style>