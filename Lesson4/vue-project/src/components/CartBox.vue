<!-- Разработать интерфейс корзины товаров, в котором пользователь может применять количество товаров в корзине и
видеть общую сумму покупки. Каждый товар представлен в виде блока, содержащего поле ввода для изменений
количества товара и отображение его цены. При изменении количества товаров в поле ввода, необходимо
автоматически пересчитывать стоимость каждого товара и обновлять общую сумму покупки. -->

<template>
    <div>
        <h2>Корзина</h2>
        <div class="goods">
            <div class="good" v-for="(good, index) in goods" :key="index">
                <input @change="updateTotal" v-model="good.amount" type="number">
                <p>Price: {{ good.price }}</p>
                <p>Subtotal: {{ good.amount * good.price }}</p>
            </div>
        </div>
        <p>Total: {{ total }}</p>
    </div>
</template>

<script>
export default {
    name: 'cart-box',

    data() {
        return {
            goods: [
                { amount: 2, price: 10 },
                { amount: 2, price: 15 },
            ],
            total: 0,
            amountGoods: '',
        };
    },

    mounted() {
        this.updateTotal();
    },

    methods: {
        updateTotal() {
            this.total = this.goods.reduce((acc, item) => {
                return acc + item.amount * item.price
            }, 0);
        }
    },
};
</script>

<style lang="scss" scoped></style>