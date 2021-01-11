<template>
  <div class="section">
    <Search/>
    <div class="columns">
      <Movies v-model="movies" />
    </div>
    
  </div>
</template>

<script>
import Search from './components/Search'
import Movies from './components/Movies'

export default {
  name: 'App',
  components: {
    Search,
    Movies
  },
  data() {
    return {
      movies: []
    }
  }
}
</script>

<style >
  @import url('https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;500;700&display=swap');
  
</style>
