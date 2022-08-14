<template>
  <div class="card d-flex" :style="{backgroundImage: 'url('+video.poster+')'}" @mouseenter="hover = true"
    @mouseleave="hover=false">
    <div class="text-white b-sm-gray h-100 text-center d-flex flex-column justify-content-center" v-if="hover">
      <h3>{{video.title}}</h3>
      <div>Titolo Originale: {{video.originalTitle}}</div>
      <div>Lingua:
        <FlagIcon :lang="video.language" />
      </div>
      <div>Voto: <span v-for="n in 5" :key="'s'-n" :class="n <= stars ? 'e-yellow' : 'e-white'">★</span></div>
    </div>
  </div>
</template>

<script>
import FlagIcon from './FlagIcon.vue'
export default {
  name: 'VideoCard',
  props: ['video'],
  data: function () {
    return { hover: false }
  },
  components: {
    FlagIcon
  },
  computed: {
    stars () {
      return Math.ceil(this.video.vote / 2)
    }
  }
}
</script>

<style>

.card{
  min-height: 513px;
  width: 342px;
  margin: 1em;
  background-color: black;
  background-size: contain;
  background-position: center;
  background-repeat: no-repeat;
}
.b-sm-gray{
  background-color: rgba(30,30,30,0.6);
}
.e-yellow{
    color: transparent;
    text-shadow: 0 0 0 yellow;
}
.e-white{
    color: transparent;
      text-shadow: 0 0 0 white;
}
</style>
