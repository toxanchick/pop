<!-- # Логин и регистрация с валидацией форм 
Создайте форму для регистрации и входа на сайт с валидацией данных. 
Используйте Vue.js для проверки правильности введенных данных.  
-->
<script setup>
    import { ref } from 'vue';

    const registration = ref({
        username: '',
        email: '',
        password: ''
    });

    const login = ref({
        username: '',
        password: ''
    });

    const errors = ref({
        registration: {
            username: '',
            email: '',
            password: '',
        },
        login: {
            username: '',
            email: '',
            password: '',
        }
    });

    const register = () => {
        errors.value.registration.username = '';
        errors.value.registration.email = '';
        errors.value.registration.password = '';

        if (!registration.value.username) {
            errors.value.registration.username = 'Имя пользователя обязательно.';
        }
        if (!registration.value.email) {
            errors.value.registration.email = 'Email обязателен.';
        }
        if (!registration.value.password) {
            errors.value.registration.password = 'Пароль обязателен.';
        } else if (registration.value.password.length < 6) {
            errors.value.registration.password = 'Пароль должен быть не менее 6 символов.';
        }

        if (!errors.value.registration.username && !errors.value.registration.email && !errors.value.registration.password) {
            alert('Регистрация успешна!');
            resetRegistrationForm();
        }
    };

    const resetRegistrationForm = () => {
        registration.value = {
            username: '',
            email: '',
            password: ''
        };
    };

    const logIn = () => {
        errors.value.registration.username = '';
        errors.value.registration.email = '';
        errors.value.registration.password = '';

        if (registration.value.username === login.value.username) {
            errors.value.login.username = 'Имя не совпадают';
        }
        
        if (registration.value.password === login.value.password) {
            errors.value.login.password = 'пароли не совпадают';
        } 

        if (!errors.value.registration.username && !errors.value.registration.email && !errors.value.registration.password) {
            alert('Вход успешна!');
            resetLoginForm();
        }
    };
</script>

<template>
    <div class="container">
        <h1>Логин и Регистрация</h1>
        <div>
            <h2>Регистрация</h2>
            <form @submit.prevent="register">
                <div>
                    <label for="regUsername">Имя пользователя:</label>
                    <input id="regUsername" type="text" v-model="registration.username" required />
                    <span v-if="errors.registration.username">{{ errors.registration.username }}</span>
                </div>
                <div>
                    <label for="regEmail">Email:</label>
                    <input id="regEmail" type="email" v-model="registration.email" required />
                    <span v-if="errors.registration.email">{{ errors.registration.email }}</span>
                </div>
                <div>
                    <label for="regPassword">Пароль:</label>
                    <input id="regPassword" type="password" v-model="registration.password" required />
                    <span v-if="errors.registration.password">{{ errors.registration.password }}</span>
                </div>
                <button type="submit">Зарегистрироваться</button>
            </form>
        </div>
        <div>
            <h2>Вход</h2>
            <form @submit.prevent="logIn">
                <div>
                    <label for="loginUsername">Имя пользователя:</label>
                    <input id="loginUsername" type="text" v-model="login.username" required />
                </div>
                <div>
                    <label for="loginPassword">Пароль:</label>
                    <input id="loginPassword" type="password" v-model="login.password" required />
                </div>
                <button type="submit">Войти</button>
            </form>
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

    form {
        margin-bottom: 20px;
    }

    label {
        display: block;
        margin-bottom: 5px;
    }

    input {
        width: 100%;
        padding: 8px;
        margin-bottom: 10px;
    }

    span {
        color: red;
        font-size: 12px;
    }
</style>

