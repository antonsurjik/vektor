<script setup>
import { reactive } from 'vue';

let users = [
    { id: 1, name: 'Иван Иванов', age: 25, city: 'Москва', role: 'Администратор' },
    { id: 2, name: 'Петр Петров', age: 30, city: 'Санкт-Петербург', role: 'Пользователь' },
    { id: 3, name: 'Мария Сидорова', age: 28, city: 'Новосибирск', role: 'Модератор' },
    { id: 4, name: 'Алексей Смирнов', age: 35, city: 'Екатеринбург', role: 'Администратор' },
    { id: 5, name: 'Екатерина Иванова', age: 22, city: 'Краснодар', role: 'Пользователь' }
];

let filters = reactive({
    name: '',
    age: '',
    city: '',
    role: ''
});

let filteredUsers = () => 
    users.filter(user =>
        user.name.includes(filters.name) && (!filters.age || user.age == filters.age) && user.city.includes(filters.city) && user.role.includes(filters.role)
    );

</script>

<template>
    <article>
        <h1>Список пользователей</h1>

        <article class="filters">
            <input v-model="filters.name" placeholder="Поиск по имени" />
            <input v-model="filters.age" type="number" placeholder="Поиск по возрасту" />
            <input v-model="filters.city" placeholder="Поиск по городу" />
            <input v-model="filters.role" placeholder="Поиск по роли" />
        </article>

        <ul>
            <li v-for="user in filteredUsers()">
                <p>Имя: {{ user.name }}</p>
                <p>Возраст: {{ user.age }}</p>
                <p>Город: {{ user.city }}</p>
                <p>Роль: {{ user.role }}</p>
            </li>
        </ul>
    </article>
</template>

<style scoped>
* {
    font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
}

.filters {
    margin-bottom: 20px;
}

.filters input {
    margin-right: 10px;
    padding: 5px;
    width: 200px;
}

ul {
    list-style-type: none;
    display: flex;
    gap: 70px;
}
</style>