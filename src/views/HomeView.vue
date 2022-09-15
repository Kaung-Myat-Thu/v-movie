<template>
  <div class="home">
    <div class="relative">
      <router-link to="/movie/tt0409591">
        <img
          class="w-full h-80 object-cover"
          src="https://m.media-amazon.com/images/M/MV5BZmQ5NGFiNWEtMmMyMC00MDdiLTg4YjktOGY5Yzc2MDUxMTE1XkEyXkFqcGdeQXVyNTA4NzY1MzY@._V1_SX300.jpg"
          alt=""
        />
        <div
          class="bg-gray-800/50 text-white absolute bottom-0 right-0 left-0 p-3"
        >
          <h3 class="text-xl font-bold">Naruto</h3>
          <p class="text-lg font-semibold leading-tight">
            Naruto Uzumaki, a mischievous adolescent ninja, struggles as he
            searches for recognition and dreams of becoming the Hokage, the
            village's leader and strongest ninja.
          </p>
        </div>
      </router-link>
    </div>

    <form
      @submit.prevent="SearchMovies"
      class="flex flex-col items-center px-3 py-4 gap-3"
    >
      <input
        v-model="state.search"
        class="w-full px-3 py-4 text-white rounded-sm drop-shadow bg-gray-700/50 placeholder:text-lg placeholder:font-semibold"
        type="text"
        placeholder="What are you looking for?"
      />
      <input
        class="text-white uppercase cursor-pointer px-3 py-4 w-full max-w-xs text-center font-bold bg-emerald-500 active:bg-emerald-600 active:rounded-md rounded-md drop-shadow-sm"
        type="submit"
        value="Search"
      />
    </form>
    <!-- search list -->
    <div class="grid grid-cols-2 gap-2 gap-y-4 p-4">
      <div
        v-for="movie in state.movies"
        :key="movie.imdbID"
        class="bg-gray-900/50 rounded-br-md rounded-bl-md"
      >
        <router-link :to="'/movie/' + movie.imdbID">
          <div class="relative">
            <img
              class="h-80 object-cover"
              :src="movie.Poster"
              :alt="movie.Title"
            />
            <div
              class="absolute left-0 bottom-4 bg-emerald-500 rounded-r px-2 py-1 text-white font-semibold"
            >
              {{ movie.Type }}
            </div>
          </div>
          <div class="text-white/80 p-2">
            <div class="font-semibold">{{ movie.Year }}</div>
            <h3 class="font-bold">{{ movie.Title }}</h3>
          </div>
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
import env from "@/env";
import { reactive } from "@vue/reactivity";
export default {
  setup() {
    const state = reactive({
      movies: [],
      search: "",
    });

    function SearchMovies() {
      if (state.search != "") {
        fetch(`http://omdbapi.com/?apikey=${env.apikey}&s=${state.search}`)
          .then((res) => res.json())
          .then((data) => {
            state.movies = data.Search;
            state.search = "";
          });
      }
    }
    return {
      state,
      SearchMovies,
    };
  },
};
</script>
