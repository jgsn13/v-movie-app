<template>
  <div class="home">
    <div class="feature-card">
      <router-link to="/movie/tt0409591">
        <img
          src="http://www.hdwallpaper.nu/wp-content/uploads/2015/06/naruto-uzumaki-wallpaper-of-2015-boruto-naruto-the-movie-anime-character-naruto-wallpaper-f98598.jpg"
          alt="Naturo Poster"
          class="feature-img"
        />
        <div class="detail">
          <h3>Naturo</h3>
          <p>
            Naturo Uzumaki, a mischievous adolescent ninja, struggles as he
            searches for recognition and dreams of becoming the Hokage, the
            village's leader and strongest ninja.
          </p>
        </div>
      </router-link>
    </div>

    <form @submit.prevent="SearchMovies()" class="search-box">
      <input
        type="text"
        placeholder="What are you looking for?"
        v-model="search"
      />
      <input type="submit" value="Search" />
    </form>

    <div class="movies-list">
      <div
        class="movie"
        v-for="movie in movies"
        :key="movie.imdbID"
        v-show="movie.imdbID"
      >
        <router-link :to="'/movie/' + movie.imdbID" class="movie-link">
          <div class="product-image">
            <img :src="movie.Poster" alt="Movie Poster" />
            <div class="type">{{ movie.Type }}</div>
          </div>
          <div class="detail">
            <p class="year">{{ movie.Year }}</p>
            <h3>{{ movie.Title }}</h3>
          </div>
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
import env from "@/env.js";

export default {
  setup() {
    const search = ref("");
    const movies = ref([]);

    const SearchMovies = () => {
      if (search.value != "") {
        fetch(`http://www.omdbapi.com/?s=${search.value}&apikey=${env.apikey}`)
          .then((response) => response.json())
          .then((data) => {
            movies.value = data.Search || { error: data.Error };
            search.value = "";
          })
          .catch((err) => {
            console.log(err.Error);
          });
      }
    };

    return {
      search,
      movies,
      SearchMovies,
    };
  },
};
</script>

<style lang="scss" scoped>
.home {
  .feature-card {
    position: relative;

    .feature-img {
      display: block;
      width: 100%;
      height: 300px;
      object-fit: cover;
      position: relative;
      z-index: 0;
    }

    .detail {
      position: absolute;
      left: 0;
      right: 0;
      bottom: 0;
      background-color: rgba(#000000, 0.6);
      padding: 16px;
      z-index: 1;

      h3 {
        color: #ffffff;
        margin-bottom: 16px;
      }

      p {
        color: #ffffff;
      }
    }
  }

  .search-box {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding: 16px;

    input {
      display: block;
      appearance: none;
      border: none;
      outline: none;
      background: none;

      &[type="text"] {
        width: 100%;
        color: #ffffff;
        background-color: #664983;
        font-size: 20px;
        padding: 10px 16px;
        border-radius: 8px;
        margin-bottom: 15px;
        transition: 0.4s;

        &::placeholder {
          color: #f3f3f3;
        }

        &:focus {
          box-shadow: 0px 3px 6px rgba(#000000, 0.2);
        }
      }

      &[type="submit"] {
        width: 100%;
        max-width: 300px;
        background-color: #7348b8;
        padding: 16px;
        border-radius: 8px;
        color: #ffffff;
        font-size: 20px;
        text-transform: uppercase;
        transition: 0.4s;
        cursor: pointer;

        &:active {
          background-color: #553b80;
        }
      }
    }
  }

  .movies-list {
    display: flex;
    flex-wrap: wrap;
    margin: 0px 8px;

    .movie {
      max-width: 50%;
      flex: 1 1 50%;
      padding: 16px 8px;

      .movie-link {
        display: flex;
        flex-direction: column;
        height: 100%;

        .product-image {
          position: relative;
          display: block;

          img {
            display: block;
            width: 100%;
            height: 275px;
            object-fit: cover;
          }

          .type {
            position: absolute;
            padding: 8px 16px;
            background-color: #7348b8;
            color: #ffffff;
            bottom: 16px;
            left: 0px;
            text-transform: capitalize;
          }
        }

        .detail {
          background-color: #694983;
          padding: 16px 8px;
          flex: 1 1 100%;
          border-radius: 0px 0px 8px 8px;

          .year {
            color: #aaaaaa;
            font-size: 14px;
          }

          h3 {
            color: #ffffff;
            font-weight: 600;
            font-size: 18px;
          }
        }
      }
    }
  }
}
</style>
