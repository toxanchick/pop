<!-- # Форма с обязательными полями 
Создайте форму с валидацией: показывайте ошибку, 
если обязательное поле пустое.  
-->

<script setup>
    import { ref } from 'vue';

    const name = ref('');
    const email = ref('');
    const feedback = ref('');

    const nameError = ref('');
    const emailError = ref('');
    const feedbackError = ref('');

    const validateForm = () => {
        let isValid = true;

        nameError.value = name.value ? '' : 'Имя обязательно для заполнения.';
        emailError.value = email.value ? '' : 'Email обязателен для заполнения.';
        feedbackError.value = feedback.value ? '' : 'Вы должны оставить отзыв.';

        if (!name.value) isValid = false;
        if (!email.value) isValid = false;
        if (!feedback.value) isValid = false;

        return isValid;
    };

    const submitForm = () => {
        if (validateForm()) {
            alert('Форма успешно отправлена!');
            resetForm();
        }
    };

    const resetForm = () => {
        name.value = '';
        email.value = '';
        feedback.value = '';
        nameError.value = '';
        emailError.value = '';
        feedbackError.value = '';
    };
</script>

<template>
    <div class="container">
        <h1>Форма с валидацией</h1>
        <form @submit.prevent="submitForm">
            <div class="form-group">
                <label for="name">Имя:</label>
                <input type="text" id="name" v-model="name" :class="{ 'is-invalid': nameError }" />
                <span v-if="nameError" class="error">{{ nameError }}</span>
            </div>
            <div class="form-group">
                <label for="email">Email:</label>
                <input type="email" id="email" v-model="email" :class="{ 'is-invalid': emailError }" />
                <span v-if="emailError" class="error">{{ emailError }}</span>
            </div>
            <div class="form-group">
                <label for="feedback">Ваш отзыв:</label>
                <textarea id="feedback" v-model="feedback" :class="{ 'is-invalid': feedbackError }" ></textarea>
                <span v-if="feedbackError" class="error">{{ feedbackError }}</span>
            </div>
            <button type="submit">Отправить</button>
        </form>
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
    
    .form-group {
        margin: 15px 0;
        text-align: left;
    }
    
    input[type='text'],
    input[type='email'],
    textarea {
        width: 100%;
        padding: 10px;
        margin-top: 5px;
        border: 1px solid #ddd;
        border-radius: 5px;
    }
    
    input[type='text'].is-invalid,
    input[type='email'].is-invalid,
    textarea.is-invalid {
        border-color: red;
    }
    
    .error {
        color: red;
        font-size: 12px;
    }
    
    button {
        padding: 10px 20px;
        background-color: #4caf50;
        color: white;
        border: none;
        border-radius: 5px;
        cursor: pointer;
    }
    
    button:hover {
        background-color: #45a049;
    }
</style>
  