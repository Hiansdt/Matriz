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
  console.log(maiorNumeroDeCadaColuna.value)

  maiorNumeroDeCadaColuna.value = []

  for (let n = 0; n < colunasMatriz.value.length; n++) {

    let maiorNumero = -Infinity

    for (let i = 0; i < matriz.value.length; i++) {
      if (matriz.value[i][n] > maiorNumero) {
        maiorNumero = matriz.value[i][n]
      }
    }

    maiorNumeroDeCadaColuna.value.push(maiorNumero)
  }
}
</script>

<template>
  <div class="all">
    <input
      type="number"
      placeholder="Digite a quantidade de linhas da matriz"
      v-model="linhasMatrizEmInput"
    />
    <input
      type="number"
      placeholder="Digite a quantidade de colunas da matriz"
      v-model="colunasMatrizEmInput"
    />

    <br />

    <span>{{ linhasMatriz }}x{{ colunasMatriz }}</span>

    <br />

    <button @click="AtualizarTamanhoMatriz()">Confirmar Tamanho</button>

    <div class="matriz">
      <div class="linhas" v-for="(linha, indexLinha) in linhasMatriz" :key="indexLinha">
        <input
          type="number"
          v-for="(coluna, indexColuna) in colunasMatriz"
          :key="indexColuna"
          class="inputs"
          v-model="matriz[indexLinha][indexColuna]"
        />
      </div>

      <button @click="calcular()">Calcular</button>

      {{ matriz }}

      <br />

      {{ maiorNumeroDeCadaColuna }}
    </div>
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
