# Currency Converter

Um simples conversor de moedas desenvolvido em Vue.js. Este projeto permite que os usuários convertem valores entre diferentes moedas de forma fácil e rápida.

### Conceitos de Programação Funcional

O projeto foi desenvolvido utilizando princípios de programação funcional, incluindo:

- **Imutabilidade**: Os dados não são alterados diretamente. Em vez disso, novas versões dos dados são criadas quando alterações são necessárias.
- **Funções puras**: As funções não têm efeitos colaterais e sempre retornam o mesmo resultado para os mesmos argumentos. Por exemplo, a função que realiza a conversão de moedas é pura, pois apenas calcula o valor sem alterar qualquer estado externo.
- **Alta ordem**: Algumas funções são passadas como argumentos para outras funções, permitindo um código mais flexível e reutilizável.

## Instruções para Executar o Programa

### Pré-requisitos

Antes de executar o projeto, certifique-se de ter o Node.js e o npm instalados em seu sistema.

### Passos para Execução

1. Clone o repositório:
   ```bash
   git clone https://github.com/lucaszambam/currency-converter.git
   ```

2. Navegue até o diretório do projeto:
   ```bash
   cd currency-converter
   ```

3. Instale as dependências:
   ```bash
   npm install
   ```

4. Inicie a aplicação:
   ```bash
   npm run serve
   ```

5. Abra seu navegador e acesse [http://localhost:8080](http://localhost:8080) para ver a aplicação em funcionamento.

## Exemplos de Entrada e Saída

### Exemplo 1
- **Entrada**: 
  - Moeda de origem: USD
  - Moeda de destino: EUR
  - Valor: 100

- **Saída**: 
  - Valor convertido: 85 EUR (valores de exemplo; a saída real dependerá da taxa de câmbio atual)

### Exemplo 2
- **Entrada**:
  - Moeda de origem: GBP
  - Moeda de destino: JPY
  - Valor: 50

- **Saída**: 
  - Valor convertido: 7,000 JPY (valores de exemplo)

## Acesso ao Projeto

Você pode acessar o projeto diretamente pelo seguinte link: [Currency Converter](https://currency-converter-lucas-zambam.vercel.app/)
