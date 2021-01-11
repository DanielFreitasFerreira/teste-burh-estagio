<template>
  <div id="movies">
    <div v-if="show" class="columns is-multiline">
      <div
        class="box column is-4 m-4 has-background-dark has-text-link-light"
        v-for="movie in movies"
        v-bind:key="movie.imdbID"
      >
        <article class="media">
          <div class="media-left">
            <figure class="image is-64x64">
              <img v-bind:src="movie.Poster" />
            </figure>
          </div>
          <div class="media-content">
            <div class="content">
              <p>Título: {{ movie.Title }}</p>
              <small>Ano lançamento: {{ movie.Year }}</small>
              <br />
              <div>
                <input
                  v-on:click="details(movie.imdbID)"
                  type="button"
                  value="+ detalhes"
                />
              </div>
            </div>
          </div>
        </article>
      </div>
    </div>

    <Details :info="info" :show="show" />
  </div>
</template>

<script>
import { baseApiUrl, ApiKey } from "@/global";
import axios from "axios";
import Details from "./Details";

export default {
  name: "Movies",
  components: {
    Details,
  },
  props: {
    movies: Array,
    show: Boolean,
  },
  data() {
    return {
      info: null,
    };
  },
  methods: {
    details: function (id) {
      axios.get(`${baseApiUrl}${ApiKey}&i=${id}`).then((res) => {
        this.info = res.data;
        this.show = false;
        this.movies = true;
      });
    },
  },
};
</script>

<style>
  .columns {
    justify-content: center;
  }
  .content {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  .content small {
    margin-bottom: 15px;
  }
  .content div {
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .content input {
    background: #bd14bd;
    border: none;
    padding: 10px;
    color: #fff;
    cursor: pointer;
  }

</style>