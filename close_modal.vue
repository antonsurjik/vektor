<template>
  <article class="app">
    <h1>Список элементов</h1>
    <ul>
      <li v-for="(item, index) in items">
        {{ item }}
        <button @click="confirmDelete(index)">Удалить</button>
      </li>
    </ul>

    <article v-if="visibility_modal" class="modal">
      <article class="modal-content">
        <p>Вы уверены, что хотите удалить этот элемент?</p>
        <button @click="deleteItem">Да</button>
        <button @click="closeModal">Отмена</button>
      </article>
    </article>
  </article>
</template>

<script setup>
import { ref } from "vue";

let items = ref(["Элемент 1", "Элемент 2", "Элемент 3"]);

let visibility_modal = ref(false);
let delited_item = ref(null);

function confirmDelete(index) {
  delited_item.value = index;
  visibility_modal.value = true;
}

function closeModal() {
  visibility_modal.value = false;
  delited_item.value = null;
}

function deleteItem() {
  if (delited_item.value !== null) {
    items.value.splice(delited_item.value, 1);
  }
  closeModal();
}
</script>

<style>
.app {
  font-family: Arial, sans-serif;
  padding: 20px;
}

button {
  margin-left: 10px;
}

.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal-content {
  background-color: white;
  padding: 20px;
  border-radius: 5px;
  text-align: center;
}

.modal-content button {
  margin: 5px;
}
</style>