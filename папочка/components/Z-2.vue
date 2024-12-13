<!-- # Список пользователей с фильтрацией 
Создайте приложение, которое отображает список пользователей и позволяет фильтровать их по нескольким полям. 
У каждого пользователя должны быть несколько характеристик, таких как имя, возраст, город и роль. 
Реализуйте фильтрацию, чтобы пользователь мог искать по любому из этих полей одновременно.  
-->
<script setup>
    import { ref, computed } from 'vue';

    const users = ref([
        { id: 1, name: 'Иван', age: 25, city: 'Москва', role: 'Администратор' },
        { id: 2, name: 'Анна', age: 30, city: 'Санкт-Петербург', role: 'Пользователь' },
        { id: 3, name: 'Роман', age: 22, city: 'Екатеринбург', role: 'Пользователь' },
        { id: 4, name: 'Ольга', age: 27, city: 'Казань', role: 'Администратор' },
        { id: 5, name: 'Сергей', age: 30, city: 'Самара', role: 'Пользователь' },
    ]);

    const filters = ref({
        name: '',
        age: '',
        city: '',
        role: '',
    });

    const filteredUsers = computed(() => {
        return users.value.filter(user => {
            const matchesName = user.name.toLowerCase().includes(filters.value.name.toLowerCase());
            const matchesAge = filters.value.age ? user.age === +filters.value.age : true;
            const matchesCity = user.city.toLowerCase().includes(filters.value.city.toLowerCase());
            const matchesRole = user.role.toLowerCase().includes(filters.value.role.toLowerCase());

            return matchesName && matchesAge && matchesCity && matchesRole;
        });
    });

    const filterUsers = () => {
    };
</script>

<template>
    <div>
        <h1>Список пользователей</h1>
    
        <div class="filter">
            <input v-model="filters.name" placeholder="Поиск по имени" @input="filterUsers" />
            <input type="number" v-model="filters.age" placeholder="Возраст" @input="filterUsers" />
            <input v-model="filters.city" placeholder="Поиск по городу" @input="filterUsers" />
            <input v-model="filters.role" placeholder="Поиск по роли" @input="filterUsers" />
        </div>
    
        <div class="user-list">
            <div v-for="user in filteredUsers" :key="user.id" class="user">
                <h3>{{ user.name }}</h3>
                <p>Возраст: {{ user.age }}</p>
                <p>Город: {{ user.city }}</p>
                <p>Роль: {{ user.role }}</p>
            </div>
        </div>
    </div>
</template>

<style scoped>
    .filter {
    margin-bottom: 20px;
    }

    .user-list {
    display: flex;
    flex-direction: column;
    }

    .user {
    border: 1px solid #ccc;
    padding: 10px;
    margin-bottom: 10px;
    }
</style>