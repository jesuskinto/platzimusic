<template lang="pug">
  #app
    img(src='./assets/logo.png')
    h1 Artistas
    select(v-model="countrySeleted")
      option(v-for="contry in countries" :value="contry.value") {{ contry.name }}
    ul
      Artist(v-for="artist in artists" :artist="artist" :key="artist.mbid")
    spinner(v-show="loading")
</template>

<script>
import getArtist from './api'
import Artist from './components/Artist.vue'
import Spinner from './components/Spinner.vue'

export default {
  name: 'app',
  components: {
    Artist,
    Spinner
  },
  data () {
    return {
      artists: [],
      countries: [
        {name: 'Argentina', value: 'argentina'},
        {name: 'Colombia', value: 'colombia'},
        {name: 'España', value: 'spain'},
        {name: 'Venezuela', value: 'venezuela'}
      ],
      countrySeleted:'spain',
      loading: true
    }
  },
  methods: {
    refreshArtist() {
      this.spinner = true
      const self = this
      getArtist(self.countrySeleted)
      .then(function (artists) {
        self.loading = false
        self.artists = artists
      })
    }
  },
  mounted() {
    this.refreshArtist()
  },
  watch: {
    countrySeleted() {
      this.refreshArtist()
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
    color #2c3e50
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
