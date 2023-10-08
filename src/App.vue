<script setup>
import { ref, computed } from 'vue'

const arrayTitle = ["MI LISTA DE NUMEROS FAVORITOS"];

const count = ref(0);
const arrayNumFav = ref([]);

const increase = () => {
  console.log('Incrementar');
  count.value++;
}

const decrease = () => {
  console.log('Sesincrementar');
  count.value--;
}

const reset = () => {
  console.log('Resetear');
  count.value = 0;
}

const classCounter = computed(() => {
  if (count.value > 0) {
    return "positive";
  }
  if (count.value < 0) {
    return "negative";
  }
  if (count.value == 0) {
    return "zero";
  }
})

const addList = () => {
  arrayNumFav.value.push(count.value);
}

const disabledBtn = computed(() => {
  const numSearch = arrayNumFav.value.find((num) => num === count.value)
  if (numSearch === 0) return true;
  return (numSearch ? true : false)
})
</script>

<template>
  <div class="container text-center">

    <h1 class="title m-3">{{ arrayTitle[0].toLocaleUpperCase() }}</h1>

    <h2 :class="classCounter"> {{ count }} </h2>

    <div class="btn-group mt-3">
      <button @click="increase" class="btn btn-success">Incrementar</button>
      <button @click="decrease" class="btn btn-danger">Sesincrementar</button>
      <button @click="reset" class="btn btn-secondary">Resetear</button>
      <button @click="addList" :disabled="disabledBtn" class="btn btn-primary">Add</button>
    </div>


    <ul class="list-group mt-5">
      <li class="list-group-item" v-for="num in arrayNumFav" :key="num">
        <h2>{{ num }}</h2>
      </li>
    </ul>
  </div>
</template>

<style>
.list-group-item {
  background-color: #181818;
  color: white;
}

@media screen {
  #app {
    display: flex;
  }
}

.title {
  text-align: center;
}

.positive {
  color: green;
}

.negative {
  color: red;
}



.zero {
  color: orange;
}
</style>