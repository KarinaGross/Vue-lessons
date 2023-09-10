<!-- Создайте компонент "Аутентификация" (Authentication), который будет отображать форму входа или сообщенние об
успешной аутентификации в зависимости от переданного пропса isAuthenticated. Используйте директиву v-if для
условного отображения разных элементов в шаблоне компонента. -->

<template>
    <div>
        <input v-model="word" type="text">
        <button @click="password">Отправить</button>
        <div v-if="isAuthenticated === passwordWord">Все верно</div>
    </div>
</template>

<script>
export default {
    name: 'authentication-block',

    data() {
        return {
            isAuthenticated: false,
            word: '',
            passwordWord: ''
        };
    },

    mounted() {

    },

    methods: {
        password() {
            this.passwordWord = this.word;
        }
    },
};
</script>

<style lang="scss" scoped></style>