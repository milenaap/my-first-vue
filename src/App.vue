><script setup>

/*******************************************************************************
 * anotaciones
 * 
 * ------------------------
 * metodo flecha:
 * () => {}
 * 
 * -------------------------
 * metodo con const:
 * const nombreConst = () => {
 *   //TODO aqui va el codigo
 * }
 * 
 * -------------------------
 * hacer una constante:
 * const nombreConst = valor
 * 
 * -------------------------
 * hacer una constante reactiva:
 * const nombreConst = ref(0) -> definir con numero
 * const nombreConst = ref('') -> definir con string
 *  const nombreConst = ref([]) -> definir con array
 *  const nombreConst = ref({}) -> definir con objeto
 * 
 *******************************************************************************/





/*******************************************************************************
 * aqui va los import
 *******************************************************************************/
import {ref,computed} from 'vue'






/*******************************************************************************
 * aqui van las variables y constantes (const,let)
 *******************************************************************************/
const counter = ref(0);

const arrayFavoritos = ref([])

const name ='vue dinamico'









/*******************************************************************************
 * aqui van los metodos o funciones
 *******************************************************************************/
const reset = () => {
  counter.value = 0;
}

const decrement = () => {
  counter.value--;
}


const increment = () => {
   counter.value ++;
}


const add = () => {
  arrayFavoritos.value.push(counter.value) 
}
   
   
const bloquearBtnAdd = computed(() => {
  const numSearch = arrayFavoritos.value.find(num => num === counter.value)
  console.log(numSearch)
  //if (numSearch === 0) return true;
  //return numSearch ? true : false;
  return numSearch || numSearch === 0
})

   

const classCounter = computed (() => {
    if(counter.value === 0){
      return 'zero'
    }
    if(counter.value > 0){
      return 'positive'
    }
    if(counter.value < 0){
      return 'negative'
    }
})

   



</script>





<template>
  <div class="container text-center mt-3">
    <h1>Hola {{ name.toUpperCase()}}</h1>
    <h2 :class="classCounter">{{counter}}</h2>
    <div class="btn-group">
    <button @click="increment" class="btn btn-success">Aumentar</button>
    <button @click="decrement" class="btn btn-danger">Disminuir</button>
    <button @click="reset" class="btn btn-secondary">reset</button>
    <button @click="add" :disabled="bloquearBtnAdd" class="btn btn-primary">Añadir</button>

    </div>

    
    <ul class="list-group mt-4">
      <li
        v-for="(num, index) in arrayFavoritos"
        :key="index"
        class="list-group-item"
      >
        {{num}}
      </li>
    </ul>

  </div>
  




</template>


<style>
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

