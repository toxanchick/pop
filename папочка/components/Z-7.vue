<!-- # Простая галерея изображений 
Создайте приложение, отображающее галерею изображений. 
Реализуйте возможность переключения между изображениями с помощью стрелок «вперед» и «назад».  
-->

<script setup>
    import { ref } from 'vue';

    const images = ref([
        'https://via.placeholder.com/600x400?text=Изображение+1',
        'https://via.placeholder.com/600x400?text=Изображение+2',
        'https://via.placeholder.com/600x400?text=Изображение+3',
    ]);

    const currentIndex = ref(0);

    const nextImage = () => {
        if (currentIndex.value < images.value.length - 1) {
            currentIndex.value += 1;
        }
    };

    const previousImage = () => {
        if (currentIndex.value > 0) {
            currentIndex.value -= 1;
        }
    };
</script>

<template>
    <div class="gallery-container">
        <h1>Галерея Изображений</h1>
    
        <div class="image-display">
            <img :src="images[currentIndex]" alt="Галерея" />
        </div>
    
        <div class="navigation">
            <button @click="previousImage" :disabled="currentIndex === 0">Назад</button>
            <button @click="nextImage" :disabled="currentIndex === images.length - 1">Вперед</button>
        </div>
    
        <div class="image-indicator">
            <p>Изображение {{ currentIndex + 1 }} из {{ images.length }}</p>
        </div>
    </div>
</template>

<style scoped>
    .gallery-container {
        max-width: 600px;
        margin: auto;
        text-align: center;
    }

    .image-display {
        margin-bottom: 20px;
    }

    .image-display img {
        max-width: 100%;
        height: auto;
        border-radius: 8px;
    }

    .navigation {
        margin-bottom: 10px;
    }

    button {
        padding: 10px 15px;
        margin: 0 5px;
        border: none;
        background-color: #007BFF;
        color: white;
        border-radius: 4px;
        cursor: pointer;
    }

    button:disabled {
        background-color: #cccccc;
        cursor: not-allowed;
    }

    .image-indicator {
        font-size: 16px;
    }
</style>