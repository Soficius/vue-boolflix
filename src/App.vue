<template>
  <div class="searchbar">
    <input type="text" name="" id="" placeholder="cerca un film">
    <button type="submit">cerca</button>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'App',
  components: {
  },
  mounted () {
    console.log('axios:', axios)
  }
}
</script>

<style lang="scss">

</style>
