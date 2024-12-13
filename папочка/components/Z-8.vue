<!-- # Простой тест 
Создайте приложение, в котором пользователь отвечает на набор вопросов с вариантами ответов 
(например, множественный выбор или один вариант). 
После завершения теста отображается общее количество выбранных правильных вариантов, 
но без указания конкретных правильных ответов.  
-->

<script setup>
    import { ref } from 'vue';

    const questions = ref([
        {
            text: 'Вопрос 1: Какой язык программирования используется для создания веб-страниц?',
            options: [
                { text: 'Python', isCorrect: false },
                { text: 'JavaScript', isCorrect: true },
                { text: 'C#', isCorrect: false },
                { text: 'Java', isCorrect: false }
            ]
        },
        {
            text: 'Вопрос 2: Какой HTML-тег используется для создания гиперссылки?',
            options: [
                { text: '<link>', isCorrect: false },
                { text: '<a>', isCorrect: true },
                { text: '<href>', isCorrect: false },
                { text: '<url>', isCorrect: false }
            ]
        },
        {
            text: 'CSS используется для...',
            options: [
                { text: 'Стилизации веб-страниц', isCorrect: true },
                { text: 'Сохранения данных', isCorrect: false },
                { text: 'Создания веб-серверов', isCorrect: false },
                { text: 'Ввода пользователем', isCorrect: false }
            ]
        }
    ]);

    const userAnswers = ref([]);
    const result = ref(null);

    const submitQuiz = () => {
        let score = 0;

        questions.value.forEach((question, index) => {
            if (userAnswers.value[index] === true) { 
                score++;
            }
        });

        result.value = score;
    };
</script>

<template>
    <div class="container">
        <h1>Тестирование</h1>
        <form @submit.prevent="submitQuiz">
            <div v-for="(question, index) in questions" :key="index" class="question">
                <h2>{{ question.text }}</h2>
                <div v-for="(option, i) in question.options" :key="i">
                    <label>
                        <input type="radio" :name="'question_' + index" :value="option.isCorrect" v-model="userAnswers[index]">
                        {{ option.text }}
                    </label>
                </div>
            </div>
            <button type="submit">Завершить тест</button>
        </form>
        <div v-if="result !== null" class="result">
            Вы набрали {{ result }} из {{ questions.length }} правильных ответов.
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
        background: white;
        padding: 15px;
        border-radius: 5px;
        box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        color: black;
    }

    .question {
        margin-bottom: 20px;
    }

    .result {
        margin-top: 20px;
        font-size: 1.5em;
        font-weight: bold;
        text-align: center;
    }
</style>