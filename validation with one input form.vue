<template>
  <article class="form-container">
    <h1>Форма с валидацией</h1>
    <form @submit.prevent="submitForm">
      <article class="form-group">
        <label for="phone">Номер телефона:</label>
        <input
          type="text"
          id="phone"
          v-model="phone"
          placeholder="Введите ваш номер телефона"
          class="input"
          maxlength="11"
        />
        <span v-if="phoneError" class="error">{{ phoneError }}</span>
      </article>
      <article class="form-group">
        <label for="message">Сообщение:</label>
        <textarea
          id="message"
          v-model="message"
          placeholder="Введите ваше сообщение"
          class="textarea"
        ></textarea>
      </article>
      <button type="submit" class="submit-button">Отправить</button>
    </form>
  </article>
</template>

<script setup>
import { ref } from "vue";
let phone = ref("");
let message = ref("");
let phoneError = ref("");

function validateForm() {
  phoneError.value = "";

  if (!phone.value.trim()) {
    phoneError.value = "Поле 'Номер телефона' обязательно для заполнения.";
    return false;
  }
  if (phone.value.length !== 11) {
    phoneError.value = "Номер телефона должен содержать 11 символов.";
    return false;
  }

  return true;
}
function submitForm() {
  if (validateForm()) {
    alert("Форма успешно отправлена!");
    phone.value = "";
    message.value = "";
  }
}
</script>

<style>
.form-container {
  font-family: Arial, sans-serif;
  max-width: 400px;
  margin: 50px auto;
  padding: 20px;
  border: 1px solid #ddd;
  border-radius: 5px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}

h1 {
  text-align: center;
  margin-bottom: 20px;
}

.form-group {
  margin-bottom: 20px;
}

label {
  display: block;
  font-weight: bold;
  margin-bottom: 5px;
}

.input,
.textarea {
  width: 100%;
  padding: 10px;
  font-size: 16px;
  border: 1px solid #ddd;
  border-radius: 5px;
}

.textarea {
  height: 100px;
  resize: none;
}

.error {
  color: red;
  font-size: 14px;
  margin-top: 5px;
  display: block;
}

.submit-button {
  width: 100%;
  padding: 10px;
  font-size: 16px;
  color: white;
  background-color: #007bff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.submit-button:hover {
  background-color: #0056b3;
}
</style>