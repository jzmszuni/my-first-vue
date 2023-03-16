<template>
  <div class="container text-center">
    <h1>{{ name.toUpperCase() }}</h1> 
    <div class="mt-2 btn-group" >
      <button 
        @click="decrement()"
        class="btn btn-sm btn-outline-primary"
      >
        decremento
      </button>
      <button 
        @click="resetNumber()"
        class="btn btn-sm btn-outline-primary"
      >
        reset
      </button>
      <button 
        @click="increment()"
        class="btn btn-sm btn-outline-primary"
      >
        incremento
      </button>
      <button 
        @click="addArray()" :disabled="disabled"
        class="btn btn-sm btn-outline-primary"
      >
        favorito
      </button>
    </div>
    <br>
    <p><span :style="changeColor">{{ numberPlus }}</span></p>
    <div class="mt-2">
      <p>Mis numeros favoritos son:
        <ul class="list-group list-group-flush">
          <li
            v-for="(myNum, index) in arrayNum" 
            :key="index"
            class="list-group-item list-group-item-action bg-dark bg-gradient text-light"
          >
            {{ myNum }}
          </li>
        </ul>
      </p>
    </div>
  </div>
</template>

<script setup>
  import { ref, computed } from "vue";
  const name = "Vue Dinamico by Sergio";
  const numberPlus = ref(0);

  const arrayNum = ref([]);
  const disabled = computed (() => {
    const numSearch = arrayNum.value.find(num => num === numberPlus.value)
    return numSearch || numSearch === 0 ? true : false
  })
  const addArray = () => {
    arrayNum.value.push(numberPlus.value)
    return arrayNum.value
  }

  // cambio de color
  const changeColor = computed(() => {
    if (numberPlus.value < 0) {
      return "color: red;";
    }else if (numberPlus.value > 0) {
      return "color: green;";
    } else {
      return "";
    }
  })
  // modificar numeroPlus 
  const increment = () => numberPlus.value ++;
  const decrement = () => numberPlus.value --;
  const resetNumber = () => numberPlus.value = 0;
</script>
