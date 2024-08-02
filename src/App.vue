<script setup>
  import { reactive } from 'vue';
  const nome = "texto"
  const conta = reactive ({
    num1: 0,
    num2: 0,
    operacao: "somar",
    resposta: 0
  })

  function garantirZero() {
    if (isNaN(conta.num1)) {
      conta.num1 = 0.0;
    }
    if (isNaN(conta.num2)) {
      conta.num2 = 0.0;
    }
  }

  function calcular() {
    if (conta.operacao == "somar") {
      conta.resposta = conta.num1 + conta.num2;
    }
    else if (conta.operacao == "subtrair") {
      conta.resposta = conta.num1 - conta.num2;
    }
    else if (conta.operacao == "multiplicar") {
      conta.resposta = conta.num1 * conta.num2;
    }
    else if (conta.operacao == "dividir") {
      conta.resposta = conta.num1 / conta.num2;
    }
  }

</script>

<template>
  <body>
    <div class="container">
      <h1> Calculadora </h1>
      <form>
        <input @keyup="event => { conta.num1 = parseFloat(event.target.value); garantirZero(); calcular() }" type="number" name="num1" id="num1">
        <input @keyup="event => { conta.num2 = parseFloat(event.target.value); garantirZero(); calcular() }" type="number" name="num2" id="num2">
        <select @change="event => { conta.operacao = event.target.value; calcular() }" name="opt" id="opt">
          <option value="somar" default>+</option>
          <option value="subtrair">-</option>
          <option value="multiplicar">*</option>
          <option value="dividir">/</option>
        </select>
      </form>
      <h2>Resposta:</h2>
      <p id="resposta">
        {{  conta.resposta  }}
      </p>
    </div>
  </body>
</template>

<style scoped>

  body {
    display: flex;
    justify-content: center;

  }

  .container {
    max-width: 720px;
    width: 100%;
    background-color: #ccc;
    margin-top: 100px;
    height: 360px;
  }

  .container h1,
  .container h2 {
    font-size: 2.5em;
    text-align: center;
  }

  #resposta {
    text-align: center;
    font-size: 24px;
  }

  form {
    display: flex;
    justify-content: space-between;
  }

  .container input,
  .container select{
    margin: 16px;
    font-size: 24px;
  }
  

</style>
