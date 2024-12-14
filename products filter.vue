<template>
  <article class="container">
    <h1>Фильтрация продуктов</h1>
    <article class="filters">
      <input v-model="search.name" type="text" placeholder="Поиск по названию" class="input" />
      <input v-model="search.price" type="number" placeholder="Максимальная цена" class="input" />
      <input v-model="search.category" type="text" placeholder="Поиск по категории" class="input" />
      <select v-model="search.inStock" class="input">
        <option value="">Наличие на складе</option>
        <option value="true">В наличии</option>
        <option value="false">Нет в наличии</option>
      </select>
    </article>
    <article class="products">
      <article v-for="product in filteredProducts" class="product">
        <h3>{{ product.name }}</h3>
        <p>Цена: {{ product.price }} ₽</p>
        <p>Категория: {{ product.category }}</p>
        <p>Наличие на складе: {{ product.inStock ? 'В наличии' : 'Нет в наличии' }}</p>
      </article>
    </article>
  </article>
</template>

<script setup>
import { ref, computed } from "vue";

let products = ref([
  { id: 1, name: "Ноутбук", price: 50000, category: "Электроника", inStock: true },
  { id: 2, name: "Мышка", price: 1000, category: "Электроника", inStock: false },
  { id: 3, name: "Книга", price: 300, category: "Книги", inStock: true },
  { id: 4, name: "Смартфон", price: 20000, category: "Электроника", inStock: true },
  { id: 5, name: "Таблетка", price: 15000, category: "Электроника", inStock: false },
]);

let search = ref({
  name: "",
  price: "",
  category: "",
  inStock: "",
});

let filteredProducts = computed(() => {
  return products.value.filter((product) => {
    let matchesName = product.name.toLowerCase().includes(search.value.name.toLowerCase());
    let matchesPrice = search.value.price ? product.price <= search.value.price : true;
    let matchesCategory = product.category.toLowerCase().includes(search.value.category.toLowerCase());
    let matchesStock = search.value.inStock === "" || product.inStock.toString() === search.value.inStock;

    return matchesName && matchesPrice && matchesCategory && matchesStock;
  });
});
</script>

<style>
.container {
  font-family: Arial, sans-serif;
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
}

h1 {
  text-align: center;
  margin-bottom: 20px;
}

.filters {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.input {
  padding: 10px;
  font-size: 16px;
  border: 1px solid #ddd;
  border-radius: 5px;
}

.products {
  margin-top: 20px;
}

.product {
  background-color: #f9f9f9;
  padding: 15px;
  margin-bottom: 10px;
  border-radius: 5px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}

.product h3 {
  margin: 0 0 10px;
}

.product p {
  margin: 5px 0;
}
</style>