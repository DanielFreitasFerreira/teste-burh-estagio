<template>
  <div class="field" id="search">
    <div class="search__control">
      <label class="label">Buscar título de filmes:</label>
        <input
          class="input"
          v-model="text"
          v-on:keyup.enter="search"
          type="text"
          required
          autofocus
        />

        <input
          class="button is-primary is-fullwidth"
          type="submit"
          v-on:click="search"
          value="Buscar"
        />
    </div>

    <div class="p-2 m-2" v-if="error != null">
      <div class="notification is-danger">
        <button class="delete" v-on:click="hideAlert"></button>
        Filme não encontrado!
      </div>
    </div>

    <Movies :movies="movies" :show="show" />
  </div>
</template>
<script>
import axios from "axios";
import { baseApiUrl, ApiKey } from "@/global";
import Movies from "./Movies";
export default {
  name: "Search",
  data: function () {
    return {
      text: "",
      movies: [],
      show: false,
      error: null,
    };
  },
  components: {
    Movies,
  },
  methods: {
    search: function () {
      axios.get(`${baseApiUrl}${ApiKey}&s=${this.text}`).then((res) => {
        if (res.data.Response == "False") {
          this.error = res.data.Error;
          this.text = "";
          this.movies = [];
        } else {
          this.movies = res.data.Search;
          this.error = null;
          this.show = true;
          this.text = "";
        }
      });
    },
    hideAlert: function () {
      this.error = null;
    },
  },
};
</script>
<style scoped>
  .label {
    text-align: center;
  }
  #search {
    margin: 20px;
    display: flex;
    flex-direction: column;
    /* margin-top: 40vh;
    transition: margin 1s;
    justify-content: center; */
  }
  .search__control {
    max-width: 800px;
    margin: 0 auto;
  }
  .is-fullwidth {
    margin: 8px 0 20px 0;
  }
</style>