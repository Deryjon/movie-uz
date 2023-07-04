<template>
  <main>
    <header class="header">
      <img src="../assets/logo.svg" class="header-logo" alt="" />
      <h2>My Favourite Movies</h2>
    </header>
    <div class="tabs ">
      <button
      class="w-[70px] md:w-[100px] h-[30px] md:h-[50px]"
        :class="['btn', { btn_green: movieStore.activeTab === 1 }]"
        @click="setTab(1)"
      >
        Favourite
      </button>
      <button
      class="w-[70px] md:w-[100px] h-[30px] md:h-[50px]"
        :class="['btn', { btn_green: movieStore.activeTab === 2 }]"
        @click="setTab(2)"
        >
        Search
      </button>
    </div>
    <div class="movies" v-if="movieStore.activeTab === 1">
      <div class="">
        <h3 class="ml-[80px] mb-2 ">Watched Movies (count: {{ movieStore.watchedMovies.length }})</h3>
        <Movie
          v-for="movie in movieStore.watchedMovies"
          :key="movie.id"
          :movie="movie"
        />
      </div>
      <h3 class="ml-[80px] mb-2 ">All Movies (count: {{ movieStore.totalCountMovies }})</h3>
      <Movie
        v-for="movie in movieStore.movies"
        :key="movie.id"
        :movie="movie"
      />
    </div>
    <div class="search" v-else>
      <Search/>
    </div>
  </main>
</template>

<script setup>
import Search from "../components/Search.vue";
import Movie from "../components/Movie.vue";
import { useMovieStore } from "../stores/MovieStore";

const setTab = (id) => {
  movieStore.setActiveTab(id)
}

const movieStore = useMovieStore();
</script>
<style>
.header {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 20px;
}
.header-logo {
  max-width: 50px;
  margin-right: 10px;
}
.btn {
  border: none;
  font-size: 14px;
  margin: 0 10px;
  border-radius: 10px;
  cursor: pointer;
  background: #efefef;
}
.btn:hover {
  opacity: 0.7;
}
.btn_green {
  background: #37df5c;
}
.tabs {
  display: flex;
  justify-content: center;
  margin-bottom: 30px;
}
</style>
