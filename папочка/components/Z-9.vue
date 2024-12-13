<!-- # Список постов с лайками и дизлайками 
Создайте приложение, которое отображает список постов. У каждого поста есть кнопки «Лайк» и «Дизлайк», 
а также счетчики для подсчета количества лайков и дизлайков. 
Реализуйте возможность для пользователя взаимодействовать с каждым постом отдельно.  
-->

<script setup>
    import { ref } from 'vue';

    const posts = ref([
        { id: 1, title: 'Первый пост', content: 'Это содержимое первого поста.', likes: 0, dislikes: 0 },
        { id: 2, title: 'Второй пост', content: 'Это содержимое второго поста.', likes: 0, dislikes: 0 },
        { id: 3, title: 'Третий пост', content: 'Это содержимое третьего поста.', likes: 0, dislikes: 0 }
    ]);

    const increaseLikes = (index) => {
        posts.value[index].likes++;
    };

    const increaseDislikes = (index) => {
        posts.value[index].dislikes++;
    };
</script>

<template>
    <div class="container">
        <h1>Список постов</h1>
        <div v-for="(post, index) in posts" :key="post.id" class="post">
            <h2>{{ post.title }}</h2>
            <p>{{ post.content }}</p>
            <div class="buttons">
                <button @click="increaseLikes(index)">Лайк ({{ post.likes }})</button>
                <button @click="increaseDislikes(index)">Дизлайк ({{ post.dislikes }})</button>
            </div>
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

    .post {
        margin-bottom: 20px;
        padding: 15px;
        border: 1px solid #ddd;
        border-radius: 5px;
        background: #fafafa;
    }

    .buttons {
        margin-top: 10px;
    }

    button {
        margin-right: 10px;
    }
</style>