<!-- # Список покупок 
Создайте приложение, позволяющее добавлять, 
редактировать и удалять элементы списка покупок.  
-->

<script setup>
    import { ref } from 'vue';

    const shoppingList = ref([]);
    const newItem = ref('');
    const isEditing = ref({});

    const addItem = () => {
        if (newItem.value.trim()) {
            shoppingList.value.push({ id: Date.now(), name: newItem.value });
            newItem.value = '';
        }
    };

    const editItem = (index) => {
        isEditing.value[index] = true;
    };

    const saveItem = (index) => {
        isEditing.value[index] = false;
    };

    const deleteItem = (index) => {
        shoppingList.value.splice(index, 1);
    };
</script>

<template>
    <div class="container">
        <h1>Список покупок</h1>
        <input v-model="newItem" @keyup.enter="addItem" placeholder="Добавить элемент..." />
        <ul>
            <li v-for="(item, index) in shoppingList" :key="item.id">
                <span v-if="!isEditing[index]">{{ item.name }}</span>
                <input v-if="isEditing[index]" v-model="item.name" @keyup.enter="saveItem(index)" @blur="saveItem(index)" />
                <button @click="editItem(index)" v-if="!isEditing[index]">Редактировать</button>
                <button @click="saveItem(index)" v-if="isEditing[index]">Сохранить</button>
                <button @click="deleteItem(index)">Удалить</button>
            </li>
        </ul>
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
        max-width: 400px;
        margin: auto;
        background: white;
        padding: 15px;
        border-radius: 5px;
        box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        color: black;
    }

    input {
        width: calc(100% - 20px);
        padding: 10px;
        margin-bottom: 10px;
    }

    ul {
        list-style: none;
        padding: 0;
    }

    li {
        padding: 10px;
        border-bottom: 1px solid #ddd;
        display: flex;
        justify-content: space-between;
        align-items: center;
    }

    button {
        margin-left: 5px;
    }
</style>