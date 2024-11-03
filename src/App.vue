<template>
    <div class="header">
        <h1>Currency Converter</h1>
        <p>Aluno: Lucas Zambam</p>
    </div>
    <CurrencyConverter />
</template>

<script>
import CurrencyConverter from './components/CurrencyConverter.vue'

export default {
  name: 'App',
  components: {
    CurrencyConverter
  }
}
</script>

<style>
#app {
    display: flex;
    align-items: center;
    height: 100vh;
    flex-direction: column;
    font-family: Roboto Mono;
}

body {
    background-color: #0d1117;
    min-height: 100vh;
    margin: 0;
    width: 100vw;
}

.header {
    width: 100%;
    background-color: #010409;
    height: 8.5rem;
    border-bottom: 2px solid #21262d;
    display: flex;
    color: white;
    place-content: center;
    align-items: center;
    display: flex;
    flex-direction: column;
}

h1 {
    font-style: italic;
    margin: 0;
    font-size: 40px;
}
</style>
