<template>
  <div class="movie-detail">
    <h2>{{ movie.Title }}</h2>
    <p class="year">{{ movie.Year }}</p>
    <img
      :src="movie.Poster"
      :alt="movie.Title + 'Poster'"
      class="featured-img"
    />
    <p class="short-info">
      <b>Rating: </b><i>{{ movie.imdbRating }}</i> <b>Votes: </b
      ><i>{{ movie.imdbVotes }}</i>
    </p>
    <p class="short-info">
      <b>Runtime:</b> <i>{{ movie.Runtime }}</i>
    </p>
    <p class="plot">
      <b><i>Plot:</i></b
      ><br />{{ movie.Plot }}
    </p>
  </div>
</template>

<script>
import { ref, onBeforeMount } from "vue";
import { useRoute } from "vue-router";
import env from "@/env.js";

export default {
  setup() {
    const movie = ref({});
    const route = useRoute();

    onBeforeMount(() => {
      fetch(
        `http://www.omdbapi.com/?i=${route.params.id}&plot=full&apikey=${env.apikey}`
      )
        .then((response) => response.json())
        .then((data) => {
          movie.value = data || { error: data.Error };
        });
    });

    return {
      movie,
      route,
    };
  },
};
</script>

<style lang="scss" scoped>
.movie-detail {
  padding: 16px;

  h2 {
    color: #ffffff;
    font-size: 28px;
    font-weight: 600;
    margin-bottom: 16px;
  }

  .featured-img {
    display: block;
    max-width: 200px;
    margin-bottom: 16px;
  }

  p {
    color: #ffffff;
    font-size: 18px;
    line-height: 1.4;
  }

  .year {
    color: #aaaaaa;
    font-size: 14px;
    margin-bottom: 16px;
  }

  .short-info,
  .plot {
    margin-top: 8px;
  }
}
</style>
