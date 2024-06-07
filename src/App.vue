<script setup>

import { ref, computed } from 'vue';

const name = "Vue dinamico";
const styleColor = "color: blue";
const arrayColores = ["blue", "red", "peru"];
const activo = false;
const arrayFrutas2 = ["🍎", "🍌", "🍉", "🍓", "🍒"];
const arrayFrutas3 = [
  {
    name: "Manzana",
    price: "$1.00",
    description: "Una manzana",
  },
  {
    name: "Pera",
    price: "$2.00",
    description: "Una pera",
  },
  {
    name: "Naranja",
    price: "$3.00",
    description: "Una naranja",
  },
];
const arrayFrutas = [
  {
    name: "Manzana",
    price: "$1.00",
    description: "Una manzana",
    stock: 0,
  },
  {
    name: "Pera",
    price: "$2.00",
    description: "Una pera",
    stock: 10,
  },
  {
    name: "Naranja",
    price: "$3.00",
    description: "Una naranja",
    stock: 20,
  },
];
const objetoFruta = {
  name: "Manzana",
  price: "$1.00",
  description: "Una manzana",
  id: 1,
};

// Metodo - methods
//const handleClick = (message) => {
// console.log(message);
//}

// ref es una funcion que permite definir una variable como reactiva, dicha funcion retorna un objeto al cual tendremos
// que acceder mediante el .value si estamos en un script, pero si estamos en el area del template no es necesario
const counter = ref(0);
const arrayFavoritos = ref([]);

const increment = () => counter.value++;

const decrement = () => counter.value--;

const reset = () => (counter.value = 0);

const classCounter = computed(() => {
  if (counter.value === 0) {
    return 'zero'
  }
  if (counter.value > 0) {
    return 'positive'
  }
  if (counter.value < 0) {
    return 'negative'
  }
});

const add = () => {
  arrayFavoritos.value.push(counter.value);
};

const bloquearBtnAdd = computed(() => {
  const numSearch = arrayFavoritos.value.find(num => num === counter.value)
  //if(numSearch === 0) return true;
  //return numSearch ? true : false;
  return numSearch || numSearch === 0;
})
</script>

<template>
  <!--Vue permite utilizar en el template funciones de javascript que tengan un retorno inmediato-->

  <!--Permite utilizar propiedades de javascript 
  <h1>Hola {{ name.toUpperCase() }}</h1>
  -->

  <!--Permite imprimir como un string un array para visualizar el contenido
  <h2>{{ arrayColores }}</h2>
-->

  <!--<h2 v-bind:style="styleColor">Soy azul</h2> // manera larga, la abreviacion es la siguiente-->
  <!--<h2 :style="styleColor">Soy azul</h2>-->
  <!--Se puede interpolar con los strings aprovechando las bondades de v-bind

  <h2 :style="`color: ${arrayColores[2]}`">Soy Peru</h2>

  -->

  <!--No se pueden utilizar if, pero como Vue acepta codigo JS, podemos utilizar un ternario
  <h2>
    {{ activo ? "Estoy activo" : "Estoy inactivo" }}
  </h2>
  -->

  <!-- DIRECTIVA V-IF 
  
  <h2 v-if="activo">
    <span>Icono</span>
    Estoy activo</h2>
  <h2 v-else-if="activo === false">Estoy inactivo</h2>
  <h2 v-else="activo">Estoy indeciso</h2>
  
  -->

  <!-- DIRECTIVA V-SHOW || Modifica el display del css
     
    <h2 v-show="activo">Estoy activo v-show</h2>
    
    -->

  <!-- DIRECTIVA V-FOR -->
  <!--
        <li v-for="(fruta, index) in arrayFrutas2" :key="index">
          {{ index }} - {{ fruta }}
        </li>

        <li v-for="fruta in arrayFrutas3" :key="fruta.name">
          {{ fruta.name }} - {{ fruta.price }} - {{ fruta.description }}
        </li>

        <li v-for="(value, propiedad, index) in objetoFruta" :key="value">
        {{index}} - {{ propiedad }} : {{ value }}
        </li>
      -->
  <!-- DATAZO: para utilizar el v-for con el v-if se puede usar el template, que es un elemento casi inexistente, 
     como el fragment en React
     <ul>
    <template v-for="item in arrayFrutas" :key="item.name">
      <li v-if="item.stock > 0">{{ item.name }} - {{ item.price }}</li>
    </template>
</ul>
-->

  <!-- Usando el metodo handleClick
      <button v-on:click.right.prevent="handleClick('texto Right')">Activame right</button>
        <button @click="handleClick('texto Left')">Activame left</button>
        <button @click.middle="handleClick('texto Middle')">Activame middle</button>
    -->
  <div class="container text-center mt-3">
    <h1>Hola {{ name.toUpperCase() }}</h1>
    <h2 :class="classCounter">{{ counter }}</h2>
    <div class="btn-group">
      <button @click="increment" class="btn btn-success">Aumentar</button>
      <button @click="decrement" class="btn btn-danger">Disminuir</button>
      <button @click="reset" class="btn btn-secondary">Reset</button>
      <button @click="add" :disabled="bloquearBtnAdd" class="btn btn-primary">Add</button>    
    </div>
    <br/><br/>
    <h2>Mis favoritos</h2>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="(num, index) in arrayFavoritos" :key="index">
        {{ num }}
      </li>
    </ul>
  </div>

</template>

<style>
h1 {
  color: red;
}

.positive {
  color: green;
}

.negative {
  color: red;
}

.zero {
  color: peru;
}
</style>
