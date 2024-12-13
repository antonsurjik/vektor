<script setup>
import { ref } from 'vue';

let text_inp = ref("")
let list_tasks = ref([])

function deleteTask(id_task) {
    list_tasks.value.splice(id_task, 1)
}

function addTask() {
    list_tasks.value.push({ text: text_inp, completed: false })
    text_inp = ""
}

function taskIsChecked(id_task) {
    list_tasks.value[id_task].completed = true
}
// import HelloWorld from './components/HelloWorld.vue'
</script>

<template>
    <section>
        <article class="inp-btn">
            <input type="text" v-model="text_inp">
            <button @click="addTask">Добавить</button>
        </article>
        <ul>
            <li v-for="(task, id_task) in list_tasks">
                <article :class="{ 
                    completed: task.completed 
                }">{{ task.text }}</article>
                <button @click="deleteTask(id_task)">Удалить</button>
                <button @click="taskIsChecked(id_task)">Выполнено</button>
            </li>
        </ul>
    </section>
</template>

<style scoped>
* {
    margin: 0;
    padding: 0;
    font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
    list-style-type: none;
}
.completed {
    text-decoration: line-through;
}
</style>
