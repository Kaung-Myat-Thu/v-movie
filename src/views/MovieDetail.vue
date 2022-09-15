<template>
  <div class="text-white py-5 px-3.5">
    <h2 class="font-bold text-lg">{{ movie.Title }}</h2>
    <p>{{ movie.Year }}</p>
    <img class="w-52 my-2 shadow-sm" :src="movie.Poster" :alt="movie.Title" />
    <p class="text-white/50">
      RunTime -
      <span class="text-emerald-500 font-semibold">{{ movie.Runtime }}</span>
    </p>
    <p class="leading-tight">{{ movie.Plot }}</p>
  </div>
</template>

<script>
import { ref, onBeforeMount } from "vue";
import env from "@/env";
import { useRoute } from "vue-router";
export default {
  setup() {
    const movie = ref({});
    const route = useRoute();

    onBeforeMount(() => {
      fetch(
        `http://omdbapi.com/?apikey=${env.apikey}&i=${route.params.id}&plot=full`
      )
        .then((res) => res.json())
        .then((data) => {
          movie.value = data;
        });
    });

    return {
      movie,
    };
  },
};
</script>
