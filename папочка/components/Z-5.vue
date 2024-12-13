<!-- # Уведомления с кнопкой для закрытия 
Создайте приложение, которое отображает список уведомлений. 
Каждое уведомление можно закрыть при нажатии на кнопку "Закрыть".  
-->

<script setup>
    import { ref } from 'vue';

    const notifications = ref([
        { id: 1, message: 'Уведомление 1: Привет, это тестовое уведомление!' },
        { id: 2, message: 'Уведомление 2: У вас новое сообщение.' },
        { id: 3, message: 'Уведомление 3: Напоминание о встрече в 15:00.' },
    ]);

    const closeNotification = (id) => {
        notifications.value = notifications.value.filter(notification => notification.id !== id);
    };
</script>

<template>
    <div class="notification-container">
        <h1>Уведомления</h1>
        <div v-if="notifications.length === 0" class="empty-message">
            Нет уведомлений
        </div>
        <div v-for="notification in notifications" :key="notification.id" class="notification">
            <p>{{ notification.message }}</p>
            <button @click="closeNotification(notification.id)">Закрыть</button>
        </div>
    </div>
</template>

<style scoped>
    .notification-container {
        max-width: 400px;
        margin: auto;
        padding: 20px;
        border: 1px solid #ccc;
        border-radius: 8px;
        box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
    }

    .notification {
        padding: 15px;
        margin-bottom: 10px;
        border: 1px solid #4CAF50;
        border-radius: 4px;
        background-color: #f9f9f9;
    }

    .notification p {
        margin: 0;
    }

    button {
        margin-top: 10px;
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

    .empty-message {
        text-align: center;
        color: #888;
    }

    p {
        color: black;
    }
</style>