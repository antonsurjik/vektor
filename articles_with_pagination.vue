<script setup>
import { reactive, computed } from 'vue';

let articles = [
    { id: 1, title: 'Some State', description: 'lorem ipsum' },
    { id: 2, title: 'Some State', description: 'lorem ipsum' },
    { id: 3, title: 'Some State', description: 'lorem ipsum' },
    { id: 4, title: 'Some State', description: 'lorem ipsum' },
    { id: 5, title: 'Some State', description: 'lorem ipsum' },
    { id: 6, title: 'Some State', description: 'lorem ipsum' },
]

let article_on_page = 1
let total_pages = computed(() => Math.ceil(articles.length / article_on_page))

let state = reactive({
    this_page: 1,
    status_of_article: {},
})

let pagination_articles = computed(() => {
    let start = (state.this_page - 1) * article_on_page
    let end = start + article_on_page
    return articles.slice(start, end)
})

let description_toggle = (id) => {
    state.status_of_article[id] = !state.status_of_article[id]
}

let nextPage = () => {
    if (state.this_page < total_pages.value) {
        state.this_page++
    }
}

let prevPage = () => {
    if (state.this_page > 1) {
        state.this_page--
    }
}
</script>

<template>
    <article style="width: 50%;">
        <h1>Список статей</h1>
        
        <ul>
            <li v-for="article in pagination_articles">
                <h2>{{ article.title }}</h2>
                <p>
                    {{ 
                        state.status_of_article[article.id] || article.description.length <= 100 ? article.description : article.description.slice(0, 100)
                    }}
                </p>
                <button 
                    v-if="article.description.length > 100" 
                    @click="description_toggle(article.id)"
                >
                    {{ state.status_of_article[article.id] ? "Скрыть" : "Показать" }}
                </button>
            </li>
        </ul>

        <article class="pagination">
            <button @click="prevPage">Предыдущая</button>
            <span>Страница {{ state.this_page }} из {{ total_pages }}</span>
            <button @click="nextPage">Следующая</button>
        </article>
    </article>
</template>

<style scoped>
* {
    font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
}
ul {
    list-style: none;
    padding: 0;
}

button {
    margin-top: 10px;
    padding: 5px 10px;
    cursor: pointer;
    background: none;
    border: none;
    font-size: 15px;
}

.pagination {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-top: 20px;
}
</style>