<script setup>
import { reactive } from 'vue';

let notifications = reactive([
  { id: 1, message: 'Новое сообщение', type: 'info' },
  { id: 2, message: 'Ошибка в системе', type: 'error' },
  { id: 3, message: 'Успешное выполнение операции', type: 'success' },
])

let close = (id) => {
  let index = notifications.findIndex((n) => n.id == id)
  if (index !== -1) {
    notifications.splice(index, 1)
  }
}
</script>

<template>
  <article>
    <h1>Уведомления</h1>
    <ul>
      <li
        v-for="notification in notifications"
        :class="`notification ${notification.type}`"
      >
        <span>{{ notification.message }}</span>
        <button @click="close(notification.id)">Закрыть</button>
      </li>
    </ul>
  </article>
</template>

<style scoped>
* {
  font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
}
.notification {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 10px;
  padding: 10px;
  border-radius: 5px;
  color: white;
}

.notification.info {
  background-color: #196191;
}

.notification.error {
  background-color: #ebb4ae;
}

.notification.success {
  background-color: #065225;
}

button {
  background: none;
  border: 1px solid white;
  color: white;
  padding: 5px 10px;
  cursor: pointer;
  border-radius: 3px;
}

button:hover {
  background-color: white;
  color: black;
}
</style>