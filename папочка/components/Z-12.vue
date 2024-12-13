<!-- # Звездный рейтинг 
Создайте звездный рейтинг, где пользователь 
может установить количество звезд.  
-->

<script setup>
    import { ref } from 'vue';

    const totalStars = 5; 
    const rating = ref(0);

    const setRating = (star) => {
        rating.value = star;
    };
</script>

<template>
    <div class="container">
        <h1>Звездный рейтинг</h1>
        <div class="star-rating">
            <span v-for="star in totalStars" :key="star" @click="setRating(star)" class="star" :class="{ filled: star <= rating }" > ★ </span>
        </div>
        <p>Выставленный рейтинг: {{ rating }} из {{ totalStars }}</p>
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
        text-align: center;
        background: white;
        padding: 20px;
        border-radius: 5px;
        box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        color: black;
    }

    .star-rating {
        display: flex;
        justify-content: center;
    }

    .star {
        font-size: 30px;
        cursor: pointer;
        color: #ccc;
        transition: color 0.2s;
    }

    .star.filled {
        color: #f39c12;
    }
</style>