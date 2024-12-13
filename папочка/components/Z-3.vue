<!-- # Cписок статей с пагинацией и скрытым описанием.
Создайте приложение, которое отображает список статей. 
Каждая статья содержит название, описание и кнопку для скрытия/отображения полного текста описания. 
Если описание статьи больше 100 символов, оно должно быть скрыто за кнопкой "Показать", 
а при нажатии на нее — текст должен раскрываться. Также добавьте пагинацию, чтобы на странице отображались 
только несколько статей одновременно. 
 -->

<script setup>
    import { ref, computed } from 'vue';

    const articles = ref([
        { id: 1, title: 'Статья 1', description: 'Это описание статьи 1, которое довольно длинное и содержит много информации.' },
        { id: 2, title: 'Статья 2', description: 'Это статья 2, описание которой также длинное и может занимать много места.' },
        { id: 3, title: 'Статья 3', description: 'Краткое описание статьи 3.' },
        { id: 4, title: 'Статья 4', description: 'Очень длинное описание статьи 4, которое превышает 100 символов. Эта статья содержит много информации, и ее стоит прочитать.' },
        { id: 5, title: 'Статья 5', description: 'Описание статьи 5, которое не слишком длинное.' },
        { id: 6, title: 'Статья 6', description: 'Описание статьи 6, которое, однако, довольно длинное и содержит много информации.' },
        { id: 7, title: 'Статья 7', description: 'Это очень интересная статья 7 с увлекательным содержанием.' },
        { id: 8, title: 'Статья 8', description: 'Описание статьи 8, проверка на скрытие длинного текста.' },
        { id: 9, title: 'Статья 9', description: 'Статья 9 - это интересная статья с множеством полезных идей.' },
        { id: 10, title: 'Статья 10', description: 'Статья 10 имеет много информации, которую стоит изучить.' }
    ]);

    const itemsPerPage = 3;
    const totalPages = computed(() => Math.ceil(articles.value.length / itemsPerPage));
    const currentPage = ref(1);
    const visibleDescriptions = ref([]);

    const paginatedArticles = computed(() => {
        const start = (currentPage.value - 1) * itemsPerPage;
        return articles.value.slice(start, start + itemsPerPage);
    });

    const toggleDescription = (index) => {
        visibleDescriptions.value[index] = !visibleDescriptions.value[index];
    };

    const trimmedDescription = (description) => {
        return description.slice(0, 100);
    };

    const previousPage = () => {
        if (currentPage.value > 1) {
            currentPage.value--;
    }
    };

    const nextPage = () => {
    if (currentPage.value < totalPages.value) {
        currentPage.value++;
    }
    };

    for (let i = 0; i < itemsPerPage; i++) {
        visibleDescriptions.value.push(false);
    }
</script>

 <template>
    <div>
        <h1>Список статей</h1>
    
        <div v-for="(article, index) in paginatedArticles" :key="article.id" class="article">
            <h2>{{ article.title }}</h2>
            <p>
                {{ visibleDescriptions[index] ? article.description : trimmedDescription(article.description) }}
                <span v-if="article.description.length > 100 && !visibleDescriptions[index]">
                    ... <button @click="toggleDescription(index)">Показать</button>
                </span>
                <span v-if="visibleDescriptions[index]">
                    <button @click="toggleDescription(index)">Скрыть</button>
                </span>
            </p>
        </div>
    
        <div class="pagination">
            <button @click="previousPage" :disabled="currentPage === 1">Назад</button>
            <span>Страница {{ currentPage }} из {{ totalPages }}</span>
            <button @click="nextPage" :disabled="currentPage === totalPages">Вперед</button>
        </div>
    </div>
</template>

<style scoped>
    .article {
    border: 1px solid #ccc;
    margin-bottom: 10px;
    padding: 10px;
    }

    .pagination {
    margin-top: 20px;
    }
</style>