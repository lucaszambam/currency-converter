<template>
    <div class="currency-converter">
        <form @submit.prevent="convertCurrency">
            <div style="display: flex; justify-content: space-around; gap: 15px;">
                <div>
                    <label for="fromCurrency">De: </label>
                    <select v-model="fromCurrency">
                        <option v-for="currency in currencies" :key="currency" :value="currency">
                            {{ currency }}
                        </option>
                    </select>
                </div>

                <div>
                    <label for="toCurrency">Para: </label>
                    <select v-model="toCurrency">
                        <option v-for="currency in currencies" :key="currency" :value="currency">
                            {{ currency }}
                        </option>
                    </select>
                </div>
            </div>

            <hr>

            <div style="display: flex; flex-direction: column; align-items: flex-end;">
                <div>
                    <label for="amount">Valor: </label>
                    <input type="number" step="0.01" v-model.number="amount" placeholder="Insira o valor" required />
                </div>

                <div>
                    <label for="exchangeRate">Taxa de Câmbio: </label>
                    <input type="number" step="0.01" v-model.number="exchangeRate" placeholder="Insira a taxa" required />
                </div>
            </div>

            <button type="submit">Converter</button>
        </form>

        <p v-if="convertedAmount !== null">
            Resultado: {{ amount }} {{ fromCurrency }} = {{ convertedAmount }} {{ toCurrency }}
        </p>
    </div>
</template>

<script>
export default {
    name: "CurrencyConverter",
    data() {
        return {
            currencies: ["USD", "EUR", "BRL", "JPY"],
            fromCurrency: "USD",
            toCurrency: "EUR",
            amount: null,
            exchangeRate: null,
            convertedAmount: null,
        };
    },
    watch: {
        amount() {
            this.convertedAmount = null;
        },
        exchangeRate() {
            this.convertedAmount = null;
        }
    },
    methods: {
        convertCurrency() {
            if (this.validateInputs(this.amount, this.exchangeRate)) {
                this.convertedAmount = this.calculateConversion(this.amount, this.exchangeRate);
            } else {
                alert("Por favor, insira valores válidos e positivos.");
            }
        },
        calculateConversion: (amount, rate) => (amount * rate).toFixed(2),
        validateInputs: (amount, rate) => {
            return amount > 0 && rate > 0 && !isNaN(amount) && !isNaN(rate);
        },
    }
};
</script>

<style scoped>
.currency-converter {
    margin: auto;
    text-align: center;
    background-color: #161b22;
    padding: 2rem;
    color: white;
    border-radius: 8px;
    font-size: 25px;
}

form div {
    margin-bottom: 10px;
}

button {
    padding: 5px 10px;
    font-size: 16px;
}

.currency-converter {
    max-width: 300px;
    margin: auto;
    text-align: center;
}

select,
input[type="number"] {
    width: 100%;
    padding: 12px;
    font-size: 18px;
    border: 1px solid #ccc;
    border-radius: 4px;
    box-sizing: border-box;
}

button {
    padding: 10px 15px;
    font-size: 18px;
    font-weight: bold;
    border: none;
    background-color: #4CAF50;
    color: white;
    cursor: pointer;
    border-radius: 4px;
    transition: background-color 0.3s ease;
}

button:hover {
    background-color: #45a049;
}
</style>
