<template>
  <div>
    <div class="searchbar d-flex justify-content-between bg-black">
      <img src="https://image.tmdb.org/t/p/w342/wwemzKWzjKYJFfCeiB57q3r4Bcm.png" class="m-3" />
      <div class="align-self-center m-3">
        <input v-model="searchText" @keyup.enter="getVideos" type="text" name="" id=""
          placeholder="cerca un film o serie tv">
        <button type="submit" @click.prevent="getVideos">cerca</button>
      </div>
    </div>
    <main class="d-flex flex-wrap justify-content-center">
      <VideoCard v-for="video in videos" :key="video.id" :video="video" />
    </main>
  </div>
</template>

<script>
import axios from 'axios'
import 'bootstrap/dist/css/bootstrap.min.css'
import VideoCard from './components/VideoCard.vue'
export default {
  name: 'App',
  components: {
    VideoCard
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
              vote: movie.vote_average,
              poster: 'https://image.tmdb.org/t/p/w342' + movie.poster_path
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
              poster: 'https://image.tmdb.org/t/p/w342' + serie.poster_path,
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
body{
  background-color: gray;
}
</style>
