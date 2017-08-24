<template lang="pug">
  #app
    img(src='./assets/logo.png')
    h1 {{ msg }}
    select(v-model="selectedCountry")
      option(v-for="country in countries" :value="country.value") {{ country.name }}
    spinner(v-show="loading")
    ul
      artist(v-for="artist in artists" v-bind:artist="artist" :key="artist.mbid")

</template>

<script>
import Artist from './components/Artist.vue'
import Spinner from './components/Spinner.vue'
import getArtists from './api'


export default {
  name: 'app',
  data () {
    return {
      msg: 'Arya Music',
      artists : [
        // { name: 'David Bowie' },
        // { name: 'Daft Punk' },
        // { name: 'Red Hot Chili Peppers' },
        // { name: 'AC/DC' },
      ],
      countries: [
        { name: 'Argentina', value: 'argentina'},
        { name: 'Colombia', value: 'colombia'},
        { name: 'España', value: 'spain'},
        { name: 'Chile', value: 'chile'}
      ],
      selectedCountry : 'chile',
      loading : true
    }
  },
  components: {
    Artist : Artist,
    Spinner: Spinner
  },
  methods: {
    refreshArtists() {
      const self = this
      this.loading = true
      this.artists = []
      getArtists(this.selectedCountry)
        .then(function (artists) {
          self.loading = false
          self.artists = artists
        })  
    }
  },
  mounted() {
    this.refreshArtists()
  },
  // mounted: function() {
  //   //Para hacer referencia a this, no al global.
  //   const self = this
  //   getArtists()
  //     .then(function (artists) {
  //       self.artists = artists
  //     })
  // },
  watch: {
    selectedCountry() {
      this.refreshArtists()
    }
  }
}
</script>

<style lang="stylus">
#app
  font-family 'Avenir', Helvetica, Arial, sans-serif
  -webkit-font-smoothing antialiased
  -moz-osx-font-smoothing grayscale
  text-align center
  color purple
  margin-top 60px

h1, h2
  font-weight normal

ul
  list-style-type none
  padding 0

li
  display inline-block
  margin 0 10px

a
  color #42b983
</style>
