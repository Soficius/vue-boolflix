<template>
  <div class="card d-flex" :style="{backgroundImage: 'url('+video.poster+')'}" @mouseenter="hover = true" @mouseleave="hover=false">
    <div class="text-white b-sm-gray h-100 text-center d-flex flex-column justify-content-center" v-if="hover">
      <h3>{{video.title}}</h3>
      <div>Titolo Originale: {{video.originalTitle}}</div>
      <div>Lingua: <FlagIcon :lang="video.language"/></div>
      <div>Voto: {{video.vote}}</div>
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
</style>
