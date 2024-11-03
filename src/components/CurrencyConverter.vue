<template>
    <div class="currency-converter">
        <form @submit.prevent="convertCurrency">
            <div style="display: flex; justify-content: space-around; gap: 15px;">
                <div>
                    <label for="fromCurrency">De: </label>
                    <select v-model="fromCurrency" @change="updateExchangeRate">
                        <option v-for="currency in currencies" :key="currency" :value="currency">
                            {{ currency }}
                        </option>
                    </select>
                </div>

                <div>
                    <label for="toCurrency">Para: </label>
                    <select v-model="toCurrency" @change="updateExchangeRate">
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
            // Objeto com taxas de câmbio padrão (de -> para)
            exchangeRates: {
                "USD": { "EUR": 0.85, "BRL": 5.25, "JPY": 110.00 },
                "EUR": { "USD": 1.18, "BRL": 6.15, "JPY": 130.00 },
                "BRL": { "USD": 0.19, "EUR": 0.16, "JPY": 21.13 },
                "JPY": { "USD": 0.0091, "EUR": 0.0077, "BRL": 0.047 }
            }
        };
    },
    watch: {
        // Limpa o resultado ao alterar o valor
        amount() {
            this.convertedAmount = null;
        },
        // Limpa o resultado ao alterar a taxa de câmbio
        exchangeRate() {
            this.convertedAmount = null;
        }
    },
    methods: {
        // Atualiza a taxa de câmbio com base nas moedas selecionadas
        updateExchangeRate() {
            if (this.fromCurrency && this.toCurrency) {
                // Define a taxa de câmbio com base na relação de "de" para "para"
                this.exchangeRate = this.getExchangeRate(this.fromCurrency, this.toCurrency);
            }
        },
        // Método chamado ao submeter o formulário
        convertCurrency() {
            if (this.validateInputs(this.amount, this.exchangeRate)) {
                // Chama a função para calcular a conversão e atualiza convertedAmount
                this.convertedAmount = this.calculateConversion(this.amount, this.exchangeRate);
            } else {
                alert("Por favor, insira valores válidos e positivos.");
            }
        },
        // Função pura que calcula a conversão usando a taxa e o valor fornecido
        calculateConversion: (amount, rate) => (amount * rate).toFixed(2),
        // Função pura para validar os valores de entrada
        validateInputs: (amount, rate) => {
            // Verifica se ambos os valores são positivos e não NaN
            return amount > 0 && rate > 0 && !isNaN(amount) && !isNaN(rate);
        },
        // Função pura que obtém a taxa de câmbio com base nas moedas selecionadas
        getExchangeRate(from, to) {
            return this.exchangeRates[from][to] || null;
        },
        // Função de ordem superior que transforma a lista de moedas em letras maiúsculas
        formattedCurrencies() {
            return this.currencies.map(currency => currency.toUpperCase());
        }
    },
    mounted() {
        // Define a taxa de câmbio padrão quando o componente é montado
        this.updateExchangeRate();
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
