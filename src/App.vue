<template>
  <div>
    <div class="searchbar">
      <input v-model="searchText" @keyup.enter="getVideos" type="text" name="" id="" placeholder="cerca un film o serie tv">
      <button type="submit" @click.prevent="getVideos">cerca</button>
    </div>
    <main>
      <ul v-for="video in videos" :key="video.id">
        <li>{{video.title}}</li>
        <li>{{video.originalTitle}}</li>
        <li>
          <FlagIcon :lang="video.language" />
        </li>
        <li>{{video.vote}}</li>
      </ul>
    </main>
  </div>
</template>

<script>
import axios from 'axios'
import FlagIcon from './components/FlagIcon.vue'
export default {
  name: 'App',
  components: {
    FlagIcon
  },
  data () {
    return {
      videos: [],
      searchText: '',
      apiMovies: 'https://api.themoviedb.org/3/search/movie',
      apiSeries: 'https://api.themoviedb.org/3/search/tv'
    }
  },
  methods: {
    getVideos () {
      this.videos = []
      const cMovies = {
        params: {
          api_key: '50df027645bf57ccc3ef82b89c1c311b',
          query: this.searchText
        }
      }
      const cSeries = {
        params: {
          api_key: 'e99307154c6dfb0b4750f6603256716d',
          query: this.searchText
        }
      }
      axios
        .get(this.apiMovies, cMovies)
        .then((res) => {
          const mapped = res.data.results.map((movie) => {
            return {
              id: 'm-' + movie.id,
              type: 'Movies',
              title: movie.title,
              originalTitle: movie.original_title,
              language: movie.original_language,
              vote: movie.vote_average
            }
          })
          this.videos.push(...mapped)
        })
        .catch((err) => {
          console.log(err)
        })
      axios
        .get(this.apiSeries, cSeries)
        .then((res) => {
          const mapped = res.data.results.map((serie) => {
            return {
              id: 's-' + serie.id,
              type: 'Series',
              title: serie.name,
              originalTitle: serie.original_name,
              language: serie.original_language,
              vote: serie.vote_average
            }
          })
          this.videos.push(...mapped)
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
