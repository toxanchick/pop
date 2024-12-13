<!-- # TODO-лист. 
Создайте приложение для ведения списка дел ("To-Do list"). 
В этом приложении нужно уметь добавлять задачи, отмечать их как выполненные и удалять. 
-->

<!-- 
1. Импортируем реактивность
2. Переменная для текста и массива задач
3. Функция добавления задачи, если значение переменной без пробелов(trim()) ничему не равно добавляем объект из текста задачи и выполненость. после чего отчищаем переменую текста.
6. Функция выполнения, передаем ей индекс и на основе индекса она меняет значение переменной объекта под переданным индексом.
7. Функция удаления вырезает(splice()) элемент массива объектов.
8. На инпуте используем v-modal, отображаем задачи через v-for передавая задачу и индекс. Ключ используем индекс. Условная отрисовка заголовка. через @click присваеваем функции.
-->

<script setup>
    import { ref } from 'vue';

    const inputText = ref('');
    const tasks = ref([]);

    const addTask = () => {
        if (inputText.value.trim() !== '') {
            tasks.value.push({ text: inputText.value, awesome: false });
            inputText.value = '';
        }
    };

    const toggleAwesome = (index) => {
        tasks.value[index].awesome = !tasks.value[index].awesome;
    };

    const deleteTask = (index) => {
        tasks.value.splice(index, 1);
    };
</script>

<template>
    <div>
        <section class="firstContainer">
            <h2>TODo</h2>
            <div class="box">
                <input v-model="inputText" type="text" placeholder="Введите заметку" />
                <button @click="addTask">+</button>
            </div>
        </section>
        <section id="conteiner">
            <h2>Tasks</h2>
            <section v-for="(task, index) in tasks" :key="index" class="task">
                <h3 v-if="task.awesome">done</h3>
                <h3 v-else>in progress</h3>
                <p>{{ task.text }}</p>
                <button @click="toggleAwesome(index)" class="btnForTask">done</button>
                <button @click="deleteTask(index)" class="btnForTask">del</button>
            </section>
        </section>
    </div>
</template>

<style scoped>
    .firstContainer {
        width: 800px;
        height: 400px;
    }
    .box {
        width: 720px;
        height: 280px;
        display: flex;
        justify-content: space-between;
        align-items: center;
    }
    #inp {
        width: 80%;
        height: 60px;
    }
    #buttonAddTask {
        width: 15%;
        height: 60px;
    }
    .conteiner {
        width: 800px;
        height: fit-content;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        gap: 20px;
    }
    .task {
        width: 100%;
        height: fit-content;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        background-color: white;
    }
    .btnForTask {
        width: 200px;
        height: 50px;
        text-align: center;
    }
    h3, p {
        color: black;
    }
</style>