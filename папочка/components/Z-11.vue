<!-- # Динамическое изменение размеров элемента 
Создайте приложение, где пользователь может изменять размеры 
квадрата с помощью ползунков для ширины и высоты.  
-->

<script setup>
    import { ref } from 'vue';

    const squareWidth = ref(100);
    const squareHeight = ref(100);
</script>

<template>
    <div class="container">
        <h1>Изменитель размера квадрата</h1>
        <div class="square" :style="{ width: squareWidth + 'px', height: squareHeight + 'px' }"></div>
        <div class="controls">
            <label> Ширина: <input type="range" v-model="squareWidth" min="50" max="500" /></label>
            <p>Ширина: {{ squareWidth }}px</p>
            <label> Высота: <input type="range" v-model="squareHeight" min="50" max="500" /></label>
            <p>Высота: {{ squareHeight }}px</p>
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
        text-align: center;
        background: white;
        padding: 20px;
        border-radius: 5px;
        box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        color: black;
    }

    .square {
        background-color: #4caf50;
        margin: 20px auto;
        transition: width 0.2s, height 0.2s;
    }

    .controls {
        margin-top: 20px;
    }
    label {
        display: flex;
        align-items: center;
        justify-content: space-between;
        margin: 15px 0;
    }
    input[type='range'] {
        margin-left: 10px;
    }
</style>