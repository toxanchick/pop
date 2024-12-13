<!-- # Ограничение длины текста 
Добавьте поле ввода с ограничением длины текста. 
Показывайте, сколько символов осталось.  
-->

<script setup>
    import { ref, computed } from 'vue';

    const totalStars = 5; 
    const rating = ref(0); 
    const feedback = ref(''); 
    const maxCharacters = 200; 

    const setRating = (star) => {
        rating.value = star;
    };

    const remainingCharacters = computed(() => {
        return maxCharacters - feedback.value.length;
    });
</script>

<template>
    <div class="container">
        <h1>Звездный рейтинг</h1>
        <div class="star-rating">
            <span v-for="star in totalStars" :key="star" @click="setRating(star)" class="star" :class="{ filled: star <= rating }" > ★ </span>
        </div>
        <p>Выставленный рейтинг: {{ rating }} из {{ totalStars }}</p>
        <h2>Оставьте свой отзыв:</h2>
        <textarea v-model="feedback" :maxlength="maxCharacters" placeholder="Ваш отзыв"></textarea>
        <p>Осталось символов: {{ remainingCharacters }}</p>
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
  
    textarea {
        width: 100%;
        height: 100px;
        margin-top: 10px;
        padding: 10px;
        border: 1px solid #ddd;
        border-radius: 5px;
        resize: none;
    }
</style>