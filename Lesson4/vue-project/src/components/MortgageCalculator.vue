<!-- 1. Создайте компонент MortgageCalculator с соответствующим шаблоном и скриптом
2. В шаблоне компонента разместите поля ввода для суммы кредита, процентной ставки и срока кредита, а также
элементы для отображения ежемесячного платежа и общей суммы выплаты
3. Используйте диррективу v-model для связывания введенных пользователем значений с соответствующими свойствами в компоненте
4. Создайте вычисляемое свойство monthlyPayment, которое будет вычислять ежемесячный платеж на основе введенных значений 
суммы кредита, процентной ставки и срока кредита
5. Создайте вычисляемое свойство totalPayment, которое будет вычислять общую сумму выплаты по кредиту, учитывая
ежемесячный платеж и срок кредита
6. Отобразите значения monthlyPayment и totalPayment в соответствующих элементах шаблона -->

<template>
    <div>
        <div>
            <label>
                Сумма кредита
                <input v-model="loanAmount" type="number" min="0" placeholder="Сумма кредита">
            </label>
            <br>
            <label>
                Процентная ставка
                <input v-model="interestRate" type="number" min="0" placeholder="Процентная ставка">
            </label>
            <br>
            <label>
                Срок кредита
                <input v-model="loanTerm" type="number" min="0" placeholder="Срок кредита">
            </label>
            <br>
        </div>

        <div>
            <div>
                <h2>Каждый месяц:</h2>
                <p>{{ monthlyPayment }}</p>
            </div>
            <div>
                <h2>Всего к оплате:</h2>
                <p>{{ totalPayment }}</p>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'MortgageCalculator',

    data() {
        return {
            interestRate: 0,
            loanTerm: 0,
            loanAmount: 0,
        };
    },

    mounted() {

    },

    methods: {

    },
    computed: {
        monthlyPayment() {
            const rate = this.interestRate / 100 / 12;
            const term = this.loanTerm;
            const principal = this.loanAmount;
            const numerator = rate * Math.pow(1 + rate, term);
            const denominator = Math.pow(1 + rate, term) - 1;
            const payment = principal * (numerator / denominator);
            return payment.toFixed(2);
        },
        totalPayment() {
            return this.loanTerm * this.monthlyPayment;
        }
    }
};
</script>

<style lang="scss" scoped></style>