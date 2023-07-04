<template>
  <form
    @submit.prevent="searchStore.getMovies(searchMovie)"
    class="flex justify-center gap-1 lg:gap-0"
  >
    <input
      type="text"
      class="search-input w-[250px] md:w-full mb-4"
      placeholder="Input movie"
      v-model="searchMovie"
    />
    <button class="lg:hidden mb-[15px]">
      <svg
        class=""
        xmlns="http://www.w3.org/2000/svg"
        height="1em"
        viewBox="0 0 512 512"
      >
        <!--! Font Awesome Free 6.4.0 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. -->
        <path
          d="M416 208c0 45.9-14.9 88.3-40 122.7L502.6 457.4c12.5 12.5 12.5 32.8 0 45.3s-32.8 12.5-45.3 0L330.7 376c-34.4 25.2-76.8 40-122.7 40C93.1 416 0 322.9 0 208S93.1 0 208 0S416 93.1 416 208zM208 352a144 144 0 1 0 0-288 144 144 0 1 0 0 288z"
        />
      </svg>
    </button>
  </form>
  <Loader v-if="searchStore.loader" />
  <div v-else>
    <Movie
      v-for="movie of searchStore.movies"
      :key="movie.id"
      :movie="movie"
      :is-search="true"
    />
  </div>
</template>

<script setup>
import Loader from "../components/Loader.vue";
import Movie from "../components/Movie.vue";
import { ref } from "vue";
import { useSearchStore } from "../stores/SearchStore";

const searchStore = useSearchStore();
const searchMovie = ref("");
</script>

<style scoped>
.search-input {
  border: 1px solid #e7e7e7;
  height: 40px;
  padding: 0 10px;
  border-radius: 10px;
}
</style>
