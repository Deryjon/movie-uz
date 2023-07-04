<template>
  <div class="movie-wrapper flex justify-center ">
    <div class="movie w-[250px] h-[250px] md:w-full  md:h-full md:gap-5 md:grid">
      <img
        :src="`https://image.tmdb.org/t/p/w300_and_h450_bestv2${movie.poster_path}`"
        :alt="movie.original_title"
        class="movie-img m-auto md:m-0 w-[80px] md:w-[200px] h-[80px] md:h-[200px]"
      />
      <div>
        <div class="movie-name text-[12px] md:text-[20px] mb-1 md:mb-5 ">
          {{ movie.original_title }} ({{ movie.release_date }})
        </div>
        <span class="movie-overview text-[8px] md:text-[15px] mb-2 md:mb-5">{{ movie.overview }}</span>
        <div class="movie-buttons" v-if="!isSearch">
          <button
            class="btn movie-buttons-watched w-[70px] md:w-[100px] h-[30px] md:h-[50px]"
            @click="movieStore.toggleWatched(movie.id)"
          >
            <span v-if="!movie.isWatched">Watched</span>
            <span v-else>Unwatched</span>
          </button>
          <button
            class="btn movie-buttons-delete w-[70px] md:w-[100px] h-[30px] md:h-[50px]"
            @click="movieStore.deleteMovie(movie.id)"
          >
            Delete
          </button>
        </div>
        <div class="movie-buttons" v-else>
          <button
            class="btn btn_green w-[50px] md:w-[100px] h-[30px] md:h-[50px]"
            @click="searchStore.addToUserMovies(movie)"
          >
            Add
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { useMovieStore } from "../stores/MovieStore";
import { useSearchStore } from "../stores/SearchStore";

const movieStore = useMovieStore();
const searchStore = useSearchStore();
const props = defineProps({
  movie: {
    type: Object,
    required: true,
    default: () => {},
  },
  isSearch: {
    type: Boolean,
    required: false,
    default: false,
  },
});
</script>

<style lang="css" scoped>
.movie {
  grid-template-columns: 200px 1fr;
  margin-bottom: 20px;
  border: 2px solid #efefef;
  padding: 10px;
  border-radius: 10px;
}

.movie-accept {
  margin-right: 10px;
}

.movie-img {
  object-fit: cover;
  border-radius: 50%;
}

.movie-name {
  display: flex;
  align-items: center;
}

.movie-overview {
  display: block;
}

.movie-buttons {
  display: flex;
  align-items: center;
  justify-content: center;
}

.movie-buttons-watched {
  color: #fff;
  background: #1eb4c3;
}

.movie-buttons-watched__icon {
  width: 15px;
  margin-left: 10px;
}

.movie-buttons-delete {
  color: #fff;
  background: #ff2a2a;
}
</style>
