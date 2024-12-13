<!-- # Всплывающее окно для подтверждения действия 
Создайте приложение с кнопкой для удаления элемента. 
При нажатии на кнопку должно появляться всплывающее окно (модальное окно), 
в котором пользователь должен подтвердить удаление.  
-->

<script setup>
    import { ref } from 'vue';

    const items = ref([
        { id: 1, name: 'Элемент 1' },
        { id: 2, name: 'Элемент 2' },
        { id: 3, name: 'Элемент 3' },
    ]);

    const showModal = ref(false);
    const itemIdToDelete = ref(null);

    const confirmDelete = (id) => {
        itemIdToDelete.value = id;
        showModal.value = true;
    };

    const deleteItem = () => {
        items.value = items.value.filter(item => item.id !== itemIdToDelete.value);
        closeModal();
    };

    const closeModal = () => {
        showModal.value = false;
        itemIdToDelete.value = null;
    };
</script>

<template>
    <div class="container">
        <h1>Список Элементов</h1>
        <ul>
            <li v-for="item in items" :key="item.id">
                {{ item.name }}
                <button @click="confirmDelete(item.id)">Удалить</button>
            </li>
        </ul>
        <div v-if="showModal" class="modal">
            <div class="modal-content">
                <h2>Подтверждение удаления</h2>
                <p>Вы уверены, что хотите удалить этот элемент?</p>
                <button @click="deleteItem">Да</button>
                <button @click="closeModal">Нет</button>
            </div>
        </div>
    </div>
</template>

<style scoped>
    .container {
        max-width: 400px;
        margin: auto;
        padding: 20px;
        border: 1px solid #ccc;
        border-radius: 8px;
        box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
    }

    ul {
        list-style-type: none;
        padding: 0;
    }

    li {
        padding: 10px;
        margin: 5px 0;
        border: 1px solid #ccc;
        border-radius: 4px;
        display: flex;
        justify-content: space-between;
    }

    button {
        padding: 5px 10px;
        background-color: #f44336;
        color: white;
        border: none;
        border-radius: 4px;
        cursor: pointer;
    }

    button:hover {
        background-color: #d32f2f;
    }

    .modal {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background-color: rgba(0, 0, 0, 0.5);
        display: flex;
        align-items: center;
        justify-content: center;
        z-index: 1000;
    }

    .modal-content {
        background: white;
        padding: 20px;
        border-radius: 8px;
        text-align: center;
        color: black;
    }

    .modal-content button {
        margin: 5px;
    }
</style>