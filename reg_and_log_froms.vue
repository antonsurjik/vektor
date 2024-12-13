<script setup>
import { reactive, ref } from 'vue';

let registerForm = reactive({
  name: '',
  email: '',
  password: '',
  confirmPassword: '',
})

// let loginForm = reactive({
//   login: '',
//   password: '',
// })

let error_about_name = ref('')
let error_about_password = ref('')
let error_about_confirm_password = ref('')
// let loginErrorLogin = ref('')
// let loginErrorPassword = ref('')

let validateRegister = () => {
  let valid = true

  error_about_name.value = ''
  error_about_password.value = ''
  error_about_confirm_password.value = ''

  if (!registerForm.name.trim()) {
    error_about_name.value = 'Имя обязательно'
    valid = false
  }
  if (registerForm.password.length < 8) {
    error_about_password.value = 'Пароль должен быть не менее 8 символов'
    valid = false
  }
  if (registerForm.confirmPassword !== registerForm.password) {
    error_about_confirm_password.value = 'Пароли не совпадают'
    valid = false
  }

  return valid
};

// let validateLogin = () => {
//   let valid = true

//   loginErrorLogin.value = ''
//   loginErrorPassword.value = ''

//   if (loginForm.login.length < 8) {
//     loginErrorLogin.value = 'Логин должен быть не менее 8 символов'
//     valid = false
//   }
//   if (!loginForm.password.trim()) {
//     loginErrorPassword.value = 'Пароль обязателен'
//     valid = false
//   }

//   return valid
// };

let submitRegister = () => validateRegister() ? alert("Вы зарегистрировались") : alert("Попробуйте еще раз")
// let submitLogin = () => validateLogin() ? alert("Вход выполнен") : alert("Попробуйте еще раз")
</script>

<template>
  <article>
    <h1>Регистрация</h1>
    <form @submit.prevent="submitRegister">
      <article>
        <label>Имя:</label>
        <input v-model="registerForm.name" type="text" />
        <p v-if="error_about_name" class="text_about_error">{{ error_about_name }}</p>
      </article>
      <article>
        <label>Email:</label>
        <input v-model="registerForm.email" type="email" />
      </article>
      <article>
        <label>Пароль:</label>
        <input v-model="registerForm.password" type="password" />
        <p v-if="error_about_password" class="text_about_error">{{ error_about_password }}</p>
      </article>
      <article>
        <label>Повторите пароль:</label>
        <input v-model="registerForm.confirmPassword" type="password" />
        <p v-if="error_about_confirm_password" class="text_about_error">{{ error_about_confirm_password }}</p>
      </article>
      <button type="submit">Зарегистрироваться</button>
    </form>

    <!-- <h1>Вход</h1>
    <form @submit.prevent="submitLogin">
      <article>
        <label>Логин:</label>
        <input v-model="loginForm.login" type="text" />
        <p v-if="loginErrorLogin" class="text_about_error">{{ loginErrorLogin }}</p>
      </article>
      <article>
        <label>Пароль:</label>
        <input v-model="loginForm.password" type="password" />
        <p v-if="loginErrorPassword" class="text_about_error">{{ loginErrorPassword }}</p>
      </article>
      <button type="submit">Войти</button>
    </form> -->
  </article>
</template>

<style scoped>
* {
    font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
}
.text_about_error {
  color: rgb(88, 22, 14);
  font-size: 0.9em;
}
form {
  margin-bottom: 20px;
}
article {
  margin-bottom: 10px;
}
button {
  padding: 5px 15px;
  cursor: pointer;
}
</style>