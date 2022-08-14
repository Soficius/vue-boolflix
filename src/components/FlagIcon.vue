<template>
    <span :class="'fi fi-'+language"></span>
</template>

<script>
import 'flag-icons/css/flag-icons.min.css'

export default {
  props: ['lang'],
  computed: {
    language () {
      return this.lang === 'en' ? 'us' : this.lang
    }
  }
}
</script>

<style>

</style>
