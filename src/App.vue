

<script setup>
import { ref } from 'vue';

// variable con su estrado inicial = [];
const memes = ref([]);
let allMemes = [];
// funcion para cargar datos en el arreglo vacio.
const loadData = async () => {
  const response = await fetch('https://api.imgflip.com/get_memes');
  const { data } = await response.json();
  console.log(data.memes);
  memes.value = data.memes;
  allMemes = data.memes;
}
// funcion para buscar un meme en el listado.
const searchMeme = (event) => {
  const value = event.target.value;
  memes.value = allMemes.filter((meme) => meme.name.toLowerCase().includes(value.toLowerCase()));
};
// funcion para cargar datos en el arreglo vacio.
loadData();
</script>


<template>
  <h1>Buscador de memes</h1> <br>
  <input type="text" name=""  placeholder="Busar Meme" class="form-control"
    style="width: 50%; margin: 0 auto;" 
  @input="searchMeme" />
   <br>

  <div class="container">
    <div class="row">
      <div v-for="meme in memes" v-bind:key="meme.id" class="col-12 col-md-3">
        <div class="card">
          <img v-bind:src="meme.url" class="card-img-top" alt="..." />
          <div class="card-body">
            <h5 class="card-title">{{ meme.name }}</h5>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

