<template lang="pug">
  li
    h2: a(v-bind:href="artist.url" target="_blank") {{ artist.name }}
    img(:src="artist.image[2]['#text']")

</template>

<script>
// import getArtists from './api'

export default {
  name: 'artist',
  props: ['artist']
  
}
</script>

<style lang="stylus" scope>
li
  display block
  margin 10px 0
</style>
