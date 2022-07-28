<template>
  <div class="searchbar">
    <input v-model="searchText" type="text" name="" id="" placeholder="cerca un film">
    <button type="submit" @click.prevent="getMovies">cerca</button>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'App',
  components: {
  },
  data () {
    return {
      movies: [],
      searchText: '',
      api: 'https://api.themoviedb.org/3/search/movie'
    }
  },
  methods: {
    getMovies () {
      const config = {
        params: {
          api_key: '50df027645bf57ccc3ef82b89c1c311b',
          query: this.searchText
        }
      }
      this.movies = []
      axios
        .get(this.api, config)
        .then((res) => {
          this.movies.push(...res.data.results)
        })
        .catch((err) => {
          console.log(err)
        })
    }
  }
}
</script>

<style lang="scss">

</style>
