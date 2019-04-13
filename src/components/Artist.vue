<template lang="pug">
  li
    img(:src="artist.image[2]['#text']")
    h2: a(:href="artist.url" target="_blanck") {{artist.name}}
</template>

<script>
export default {
  name: 'artist',
  props: [
    'artist'
  ]
}
</script>

<style lang="stylus">
</style>
