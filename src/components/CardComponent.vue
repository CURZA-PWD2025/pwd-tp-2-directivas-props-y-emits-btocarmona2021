<script setup lang="ts">
import type { Pelicula } from "@/interfaces/Pelicula";

const props = defineProps<{ movie: Pelicula }>();

const emit = defineEmits(["updateLikes"]);
const enviarLikes = (id: number) => {
  emit("updateLikes", id);
};
</script>

<template>
  <div class="card">
    <div class="card__titulo">
      <h2>{{ movie.titulo }}</h2>
      <h3>{{ movie.anio }}</h3>
    </div>
    <div class="card__portada">
      <img
        v-if="movie.portada"
        class="portada__imagen"
        :src="movie.portada"
        :alt="movie.titulo"
      />
      <img
        v-else
        class="portada__imagen"
        src="https://www.cucea.udg.mx/sites/default/files/styles/publicaciones/public/publicaciones/portadas/sin_portada_8.jpg?itok=yR2MLoZs"
        :alt="movie.titulo"
      />
    </div>
    <div class="card__genero">
      <h3>{{ movie.genero }}</h3>
      <h3>{{ movie.director }}</h3>
    </div>
    <div class="card__likes">
      <h3>Likes: {{ movie.likes }}</h3>
      <button
        v-if="!movie.liked"
        class="card__button--likes"
        @click="enviarLikes(movie.id)"
      >
        💖Me gusta
      </button>
      <button
        v-else
        class="card__button--likes dis"
        @click="enviarLikes(movie.id)"
      >
        💔No me gusta
      </button>
    </div>
  </div>
</template>

<style scoped>
.card {
  margin: 10px;
  width: 360px;
  height: 400px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background-color: rgb(95, 94, 95);
  border-radius: 10px;
  box-shadow: 0 0 3px 1px whitesmoke;
  transition: 0.3s;
}
.card:hover {
  transform: scale(1.05) rotate(2deg);
}
.card__portada {
  width: 360px;
  height: auto;
  display: flex;
  justify-content: center;
  align-items: center;
}
.portada__imagen {
  width: 70%;
  height: 200px;
  object-fit: fill;
  border-radius: 10px;
  border: 2px solid rgb(30, 6, 16);
  box-shadow: 0px 0px 10px rgb(66, 11, 34);
}
.portada__imagen:hover {
  animation-name: bubbles;
  animation-play-state: running;
  animation-duration: 1s;
  animation-iteration-count: 1;
}

@keyframes bubbles {
  0% {
    transform: scale(1);
    box-shadow: 0 0 1px 2px #c2185b;
  }
  50% {
    transform: scale(1.1);
    box-shadow: 0 0 5px 5px #c2185b;
  }
  100% {
    transform: scale(1);
    box-shadow: 0 0 2px 2px #c2185b;
  }
}
.card__titulo {
  width: 100%;
  display: flex;
  justify-content: space-around;
  align-items: center;
  gap: 20px;
  margin: 10px;
  background-color: rgb(1, 67, 141);
}
.card__genero {
  margin-top: 10px;
  width: 100%;
  height: auto;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background-color: rgb(30, 6, 16);
  border-radius: 5px;
  color: rgb(231, 178, 231);
}
.card__likes {
  margin-top: 5px;
  width: 100%;
  height: auto;
  display: flex;
  justify-content: space-around;
  align-items: center;
  background-color: rgb(1, 67, 141);
  border-radius: 5px;
  padding: 4px;
}
.card__button--likes {
  background-color: #e91e63; /* Rosa fuerte */
  color: white;
  border: none;
  padding: 10px 20px;
  font-size: 16px;
  font-weight: bold;
  border-radius: 25px;
  cursor: pointer;
  transition: all 0.3s ease;
  display: flex;
  align-items: center;
  gap: 8px;
  box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.2);
}

.card__button--likes:hover {
  background-color: #c2185b;
  transform: scale(1.1);
  box-shadow: 0px 6px 12px rgba(0, 0, 0, 0.3);
}

.card__button--likes:active {
  transform: scale(0.9);
}
.dis {
  background-color: #222021;
}
.dis:hover {
  background-color: #5a595a;
}
</style>
