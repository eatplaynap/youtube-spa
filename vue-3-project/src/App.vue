<template>
  <LiteYouTubeEmbed
      id="dQw4w9WgXcQ"
      title="Rick Astley - Never Gonna Give You Up (Official Music Video)"
  />
</template>

<script>
  import { defineComponent } from 'vue'
  import LiteYouTubeEmbed from 'vue-lite-youtube-embed'
  import 'vue-lite-youtube-embed/dist/style.css'

  export default defineComponent({
    components: { LiteYouTubeEmbed }
  })
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
