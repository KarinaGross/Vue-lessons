<!-- Создайте компонент, который будет отображать карточку товара с деталями и отзывами пользователей.
Пользователи могут добавлять свои отзывы и оценивать товар по 5-бальной шкале.
1. Отображение деталей товара: Название, описание, цена.
2. Список отзывов: Каждый отзыв содержит имя пользователя, текст отзыва и оценку от 1 до 5.
3. Форма добавления отзыва: Текстовое поле для имени, область текста для отзыва и выбор оценки от 1 до 5.
4. Средний рейтинг товара: Рассчитывается на основе всех оставленных оценок. -->

<template>
    <div id="app">
        <div class="good">
            <h2 class="good__name">{{ good.name }}</h2>
            <p class="good__description">{{ good.description }}</p>
            <p class="good__price">{{ good.price }}</p>
            <p>Средний рейтинг: {{ averageRating }}</p>
        </div>
        <h3>Отзывы:</h3>
        <div v-for="feedback in feedbacks" :key="feedback.id" class="feedback">
            <h2 class="feedback__name">{{ feedback.username }}</h2>
            <p class="good__rating">{{ feedback.rating }}/5</p>
            <p class="feedback__text">{{ feedback.text }}</p>
        </div>
        <h3>Добавить отзыв:</h3>
        <input v-model="username" type="text" placeholder="Ваше имя" />
        <textarea v-model="feedbackText" placeholder="Ваш отзыв"></textarea>
        <select v-model="rating">
            <option v-for="n in 5" :key="n">{{ n }}</option>
        </select>
        <button @click="submitFeedback">Отправить</button>
    </div>
</template>
  
<script>
export default {
    data() {
        return {
            good: {
                name: 'Телефон',
                description: 'Самый лучший телефон',
                price: '50000'
            },
            feedbacks: [
                {
                    id: 1,
                    username: 'Ваня',
                    text: 'Очень крутой товар',
                    rating: 5
                },
                {
                    id: 2,
                    username: 'Света',
                    text: 'Очень крутой товар',
                    rating: 4
                },
                {
                    id: 3,
                    username: 'Катя',
                    text: 'Очень крутой товар',
                    rating: 5
                }
            ],
            username: '',
            feedbackText: '',
            rating: 5
        };
    },
    methods: {
        submitFeedback() {
            const newFeedback = {
                id: Date.now(),
                username: this.username,
                text: this.feedbackText,
                rating: parseInt(this.rating)
            };
            this.feedbacks.push(newFeedback);
            this.username = '';
            this.feedbackText = '';
            this.rating = 5;
        }
    },
    computed: {
        averageRating() {
            if (this.feedbacks.length === 0) return 0;
            const sumRatings = this.feedbacks.reduce((accumulator, currentValue) => accumulator + currentValue.rating, 0);
            return (sumRatings / this.feedbacks.length).toFixed(2);

        }
    }
};
</script>
  
  <!-- Use preprocessors via the lang attribute! e.g. <style lang="scss"> -->
<style>
.good {
    padding: 10px;
    border: 1px black solid;
    text-align: center;
    width: 300px;
}

.feedback {
    border: 1px gray solid;
    padding-left: 10px;
}
</style>