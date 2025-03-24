<template>
  <h1>Hola: {{ name }}</h1>
  <button @click.right.prevent="handleClick('Hola')">Click</button>
  <!--Funciones computadas se llaman sin parentesis-->
  <h2 :class="classCounter">{{ counter }}</h2>
  <button @click="aumentarContador()">Aumentar contador</button>
  <button @click="decrementarContador()">Decrementar contador</button>
  <button @click="resetearContador()">Resetear contador</button>
  <button @click="add()" :disabled="botonDisabled">Agregar</button>
  <br />
  <ul>
    <li v-for="(num, index) in numeros" :key="index">
    {{ num }}
    </li>
  </ul>
</template>

<script setup>
import { ref, computed } from 'vue'
const name = 'Vue dinamico'
const counter = ref(0)
const numeros = ref([])
// Siempre que trabajemos con datos reactivos tenemos que trabajar con funciones computadas
const classCounter = computed(() => {
  if(counter.value === 0){
    return 'zero'
  }
  return counter.value > 0 ? 'positive' : 'negative'
})
const handleClick = (text) => {
  console.log(text)
}

const aumentarContador = () => {
  counter.value ++
}

const decrementarContador = () => {
  counter.value --
}

const resetearContador = () => {
  counter.value = 0
}

const add = () => {
  numeros.value.push(counter.value)
}

const botonDisabled = computed(() => {
  const numSearch = numeros.value.find((num) => num === counter.value)
  if(numSearch === 0) return true
  return numSearch ? true : false
})

</script>

<style>
.positive{
  color: green
}

.negative{
  color: red
}

.zero{
  color: purple;
}

</style>