<script setup>
import { ref } from 'vue'

const linhasMatrizEmInput = ref()
const colunasMatrizEmInput = ref()

const linhasMatriz = ref()
const colunasMatriz = ref()

const matriz = ref([])

const maiorNumeroDeCadaColuna = ref([])

const matrizCalculando = ref(false)

function AtualizarTamanhoMatriz() {
  linhasMatriz.value = linhasMatrizEmInput.value
  colunasMatriz.value = colunasMatrizEmInput.value

  for (let i = 0; i < linhasMatriz.value; i++) {
    matriz.value.push([])
  }
}

function calcular() {

  matrizCalculando.value = true

  setTimeout(() => {
    matrizCalculando.value = false
    console.log(colunasMatriz.value)

    maiorNumeroDeCadaColuna.value = [];

    for (let n = 0; n < colunasMatriz.value; n++) {

      console.log(n)

      let maiorNumero = -Infinity
      let maiorNumeroOriginal = -Infinity

      for (let i = 0; i < matriz.value.length; i++) {

        let numero = matriz.value[i][n]
        let numeroOriginal = matriz.value[i][n]

        if (numero < 0) {
          numero = numero * -1
        }

        if (numero > maiorNumero) {
          maiorNumero = numero
          if (numeroOriginal < 0) {
            maiorNumeroOriginal = maiorNumero * -1
          } else maiorNumeroOriginal = maiorNumero
        }
      }

      console.log(maiorNumero)

      maiorNumeroDeCadaColuna.value.push(maiorNumeroOriginal)
    }

    console.log(matriz.value)
  }, 1000);
}
</script>

<template>
  <div class="all">
    <input type="number" class="tamanho" placeholder="Digite a quantidade de linhas da matriz"
      v-model="linhasMatrizEmInput" />
    <input type="number" class="tamanho" placeholder="Digite a quantidade de colunas da matriz"
      v-model="colunasMatrizEmInput" />

    <br />

    <button @click="AtualizarTamanhoMatriz()">Confirmar Tamanho</button>

    <div class="matriz">
      <div class="linhas" v-for="(linha, indexLinha) in linhasMatriz" :key="indexLinha">
        <input type="number" v-for="(coluna, indexColuna) in colunasMatriz" :key="indexColuna"
          :class="matrizCalculando ? 'matrizCalculando' : 'inputsMatriz'" v-model="matriz[indexLinha][indexColuna]" />
      </div>
    </div>
    <button @click="calcular()">Calcular</button>

    <br />

    <div class="maioresNumeros" v-if="matrizCalculando == false">
      <span v-for="maiorNumero, index of maiorNumeroDeCadaColuna" :key="index">
        Maior Número da coluna {{ index + 1 }}:
        {{ maiorNumero }} <br>
      </span>
    </div>
  </div>
</template>

<style scoped>
.inputsMatriz {
  width: 100px;
  height: 100px;
  padding: 10px;
  margin: 10px;
  border: none;
  outline: none;
  font-family: inherit;
  font-weight: 500;
  font-size: medium;
}


.inputsMatriz:focus {
  transform: scale(1.1);
  animation: animacaoMatrizSelect 0.1s;
}

@keyframes animacaoMatrizSelect {
  0% {
    transform: scale(1);
  }

  100% {
    transform: scale(1.1);
  }
}

.matrizCalculando {
  width: 100px;
  height: 100px;
  padding: 10px;
  margin: 10px;
  border: none;
  outline: none;
  font-family: inherit;
  font-weight: 500;
  font-size: medium;
  animation: animacaoMatrizCalculando 1s linear;
}

@keyframes animacaoMatrizCalculando {
  0% {
    transform: rotate(0deg);
  }

  20% {
    transform: rotate(200deg);
  }

  40% {
    transform: rotate(600deg);
  }

  45% {
    transform: rotate(620deg);
  }

  100% {
    transform: rotate(720deg);
  }
}

.all {
  width: 180vh;
  height: 80vh;
}

button {
  background-color: blueviolet;
  appearance: none;
  color: aliceblue;
  border: 0;
  margin: 10px;
  font: inherit;
  font-size: large;
  line-height: 1;
  font-weight: 500;
  padding: 0.5em 1em;
  cursor: pointer;
  transition: filter var(--motion-duration);
}

button:hover {
  filter: brightness(1.5);
  box-shadow: 0px 0px 10px blueviolet;
  transform: rotate(1deg) scale(1.05);
  animation: hoverbotao 0.2s linear;
}

@keyframes hoverbotao {
  0% {
    filter: brightness(1);
    box-shadow: none;
    transform: rotate(0) scale(1);
  }

  100% {
    filter: brightness(1.5);
    box-shadow: 0px 0px 10px blueviolet;
    transform: rotate(1deg) scale(1.05);
  }
}

.tamanho {
  width: 350px;
  font-size: medium;
  margin: 20px;
  border: none;
  border-radius: 15px;
  height: 25px;
  padding: 15px;
  outline: none;
}

.tamanho:focus {
  transform: scale(1.1);
  box-shadow: 7px 7px 2px rgb(94, 94, 94);
  animation: animacaoInput 0.2s linear;
}

@keyframes animacaoInput {
  0% {
    transform: scale(1);
    box-shadow: none;
  }

  100% {
    transform: scale(1.1);
    box-shadow: 7px 7px 2px rgb(94, 94, 94);
  }
}

span {
  font-size: larger;
  color: white;
  animation: animacaoSpan 0.3s linear;
  width: max-content;
}

@keyframes animacaoSpan {
  0% {
    font-size: larger;
  }

  80% {
    font-size: x-large;
  }

  100% {
    font-size: larger;
  }
}
</style>
