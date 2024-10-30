<template>
  <p> compteur : {{ count }}</p>
  <button @click="increment">Incrémenter</button>
  <button @click="decrement">Décrémenter</button>

  <hr>

  <form action="" @submit.prevent="">
    <input type="text" placeholder="Nouveau Film" v-model="newMovie">
    <button @click="addMovie">Ajouter</button>
  </form>
  <button @click="sortMovies">Réorganiser</button>
  <ul>
    <li 
    v-for="movie in movies"
    :key="movie"
    >
      {{ movie }} <button @click="deleteMovie(movie)">Supprimer</button>
    </li>
  </ul>
</template>

<script setup>
import { ref } from 'vue'
const count = ref(0)

const movies = ref([
  'Matrix',
  'Lilo & Stitch',
  'Titanic'
])

const newMovie = ref('')

const deleteMovie = (movie) => {
  movies.value = movies.value.filter(m => m !== movie)
}

const sortMovies = () => {
  movies.value = movies.value.sort()
}

const addMovie = () => {
  movies.value.push(newMovie.value)
  newMovie.value = ''
}

const increment = (event) => {
  count.value++
}
const decrement = () => {
  count.value--
}
</script>

<style>
.active {
  color: red;
}
</style>