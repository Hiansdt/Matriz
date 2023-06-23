<script setup>
import { ref } from 'vue'

const linhasMatrizEmInput = ref()
const colunasMatrizEmInput = ref()

const linhasMatriz = ref()
const colunasMatriz = ref()

const matriz = ref([])

const maiorNumeroDeCadaColuna = ref([])

function AtualizarTamanhoMatriz() {
  linhasMatriz.value = linhasMatrizEmInput.value
  colunasMatriz.value = colunasMatrizEmInput.value

  for (let i = 0; i < linhasMatriz.value; i++) {
    matriz.value.push([])
  }
}

function calcular() {
  console.log(colunasMatriz.value)

  maiorNumeroDeCadaColuna.value = [];

  for (let n = 0; n < colunasMatriz.value; n++) {

    console.log(n)

    let maiorNumero = -Infinity

    for (let i = 0; i < matriz.value.length; i++) {

      let numero = matriz.value[i][n]

      if (numero < 0) {
        numero = numero * -1
      }

      if (numero > maiorNumero) {
        maiorNumero = numero
      }
    }

    console.log(maiorNumero)

    maiorNumeroDeCadaColuna.value.push(maiorNumero)
  }

  console.log(matriz.value)
}
</script>

<template>
  <div class="all">
    <input type="number" placeholder="Digite a quantidade de linhas da matriz" v-model="linhasMatrizEmInput" />
    <input type="number" placeholder="Digite a quantidade de colunas da matriz" v-model="colunasMatrizEmInput" />

    <br />

    <button @click="AtualizarTamanhoMatriz()">Confirmar Tamanho</button>

    <div class="matriz">
      <div class="linhas" v-for="(linha, indexLinha) in linhasMatriz" :key="indexLinha">
        <input type="number" v-for="(coluna, indexColuna) in colunasMatriz" :key="indexColuna" class="inputs"
          v-model="matriz[indexLinha][indexColuna]" />
      </div>
    </div>
    <button @click="calcular()">Calcular</button>

    <br />

    <span v-for="maiorNumero, index of maiorNumeroDeCadaColuna" :key="index">
      Maior Número da coluna {{ index + 1 }}:
      {{ maiorNumero }} <br>
    </span>
  </div>
</template>

<style scoped>
.inputs {
  width: 100px;
  height: 100px;
}

.all {
  width: 180vh;
  height: 80vh;
}
</style>
