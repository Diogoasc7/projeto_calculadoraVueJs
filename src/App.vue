<script setup>
  import { reactive, watchEffect } from "vue";
  import Resultado from "./components/Resultado.vue";


  const valores = reactive({
  primeiroNumero: 0,
  segundoNumero: 0,
  operacao: 'adicao',
  resultado: 0,
});

const operacoes = {
  adicao: (a, b) => a + b,
  subtracao: (a, b) => a - b,
  multiplicacao: (a, b) => a * b,
  divisao: (a, b) => b !== 0 ? a / b : 'Erro: divisão por zero'
};

function calcular() {
  const op = operacoes[valores.operacao];
  valores.resultado = op(valores.primeiroNumero, valores.segundoNumero);
}

function atualizarValor(campo, evento) {
  const valor = evento.target.value;
  if (campo === 'operacao') {
    valores.operacao = valor;
  } else {
    valores[campo] = parseFloat(valor) || 0;
  }
  calcular();
}

watchEffect(calcular);
</script>

<template>
  <div class="container py-5">
    <div class="text-center mb-5">
      <h1 class="display-5 fw-bold">Calculadora Vue</h1>
      <p class="text-muted">Realize operações matemáticas básicas</p>
    </div>

    <div class="card shadow mx-auto" style="max-width: 500px;">
      <div class="card-body p-4">
        <div class="mb-3">
          <label class="form-label">Primeiro número</label>
          <input
            type="number"
            class="form-control"
            @input="(e) => atualizarValor('primeiroNumero', e)"
            placeholder="Digite o primeiro número"
          />
        </div>

        <div class="mb-3">
          <label class="form-label">Segundo número</label>
          <input
            type="number"
            class="form-control"
            @input="(e) => atualizarValor('segundoNumero', e)"
            placeholder="Digite o segundo número"
          />
        </div>

        <div class="mb-4">
          <label class="form-label">Operação</label>
          <select class="form-select" @change="(e) => atualizarValor('operacao', e)">
            <option value="adicao">Adição (+)</option>
            <option value="subtracao">Subtração (-)</option>
            <option value="multiplicacao">Multiplicação (×)</option>
            <option value="divisao">Divisão (÷)</option>
          </select>
        </div>

        <Resultado :resultado="valores.resultado" />
      </div>
    </div>
  </div>
</template>

<style scoped>
  
</style>
