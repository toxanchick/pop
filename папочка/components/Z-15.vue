<!-- # Фильтрация продуктов по цене 
Разработайте приложение, которое показывает список товаров с различными характеристиками, 
такими как название, цена, категория и наличие на складе. Реализуйте возможность фильтрации списка, 
чтобы пользователь мог искать и отображать результаты по любому из этих полей одновременно. Например, 
при вводе названия, цены, категории или наличия на складе, товары, соответствующие условиям поиска, 
должны отображаться на экране. 
-->

<script setup>
    import { ref, computed } from 'vue';

    const products = ref([
        { id: 1, name: 'Товар 1', price: 100, category: 'Электроника', inStock: true },
        { id: 2, name: 'Товар 2', price: 200, category: 'Одежда', inStock: false },
        { id: 3, name: 'Товар 3', price: 150, category: 'Электроника', inStock: true },
        { id: 4, name: 'Товар 4', price: 300, category: 'Книги', inStock: true },
        { id: 5, name: 'Товар 5', price: 50, category: 'Канцтовары', inStock: false },
    ]);

    const filters = ref({
        name: '',
        price: null,
        category: '',
        inStock: false,
    });

    const filteredProducts = computed(() => {
        return products.value.filter(product => {
            const matchesName = product.name.toLowerCase().includes(filters.value.name.toLowerCase());
            const matchesPrice = filters.value.price === null || product.price <= filters.value.price;
            const matchesCategory = product.category.toLowerCase().includes(filters.value.category.toLowerCase());
            const matchesInStock = !filters.value.inStock || product.inStock;

            return matchesName && matchesPrice && matchesCategory && matchesInStock;
        });
    });
</script>

<template>
    <div class="container">
        <h1>Список товаров</h1>
        <div class="filters">
            <input v-model="filters.name" type="text" placeholder="Название товара" />
            <input v-model.number="filters.price" type="number" placeholder="Максимальная цена" />
            <input v-model="filters.category" type="text" placeholder="Категория" />
            <label><input type="checkbox" v-model="filters.inStock" />В наличии</label>
        </div>
        <div class="product-list">
            <div class="product" v-for="product in filteredProducts" :key="product.id">
                <h3>{{ product.name }}</h3>
                <p>Цена: {{ product.price }}₽</p>
                <p>Категория: {{ product.category }}</p>
                <p>Наличие: {{ product.inStock ? 'Да' : 'Нет' }}</p>
            </div>
        </div>
    </div>
</template>
  
<style scoped>
    body {
        font-family: Arial, sans-serif;
        background-color: #f0f0f0;
        margin: 0;
        padding: 20px;
    }
    
    .container {
        max-width: 600px;
        margin: auto;
        background: white;
        padding: 20px;
        border-radius: 5px;
        box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        color: black;
    }
    
    .filters {
        display: flex;
        flex-direction: column;
        margin-bottom: 20px;
    }
    
    .filters input[type='text'],
    .filters input[type='number'] {
        margin: 5px 0;
        padding: 10px;
        border: 1px solid #ddd;
        border-radius: 5px;
    }
    
    .product-list {
        margin-top: 20px;
    }
    
    .product {
        border: 1px solid #ddd;
        padding: 10px;
        margin: 10px 0;
        border-radius: 5px;
    }
</style>  