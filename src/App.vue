<script setup lang="ts">
import mov from "./resource/movies";
import CardComponent from "./components/CardComponent.vue";
import { ref } from "vue";

const movies = ref(mov.map((movie) => ({ ...movie, liked: false })));

const update = (id: number) => {
  movies.value.forEach((movie) => {
    if (movie.id === id) {
      if (!movie.liked) {
        movie.likes++;
      } else {
        movie.likes--;
      }
      movie.liked = !movie.liked;
    }
  });
};
</script>

<template>
  <div class="header">
    <h1>Tus peliculas favoritas</h1>
  </div>
  <div v-for="movie in movies" :key="movie.id">
    <CardComponent :movie="movie" @updateLikes="update" />
  </div>
</template>

<style scoped>
.header {
  grid-column: span 3;
  height: 100px;
  font-size: 2em;
  display: flex;
  color: rgb(201, 0, 201);
  justify-content: center;
  text-shadow: 0 0 2px whitesmoke;
  background-color: rgb(33, 20, 20);
}
</style>
