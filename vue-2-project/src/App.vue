<template>
  <div>
<!--    <youtube :video-id="videoId" ref="youtube" :playerVars="playerVars" @playing="playingVideo"></youtube>-->
    <youtube :video-id="videoId" ref="youtube" @playing="playingVideo"></youtube>
    <div>
      <button @click="pauseVideo" v-if="playing">pause</button>
      <button @click="playVideo" v-else>play</button>
    </div>
    <div>
      <label>URL:</label>
      <textarea v-model="newURL"></textarea>
      <button @click="changeVideo">change video</button>
    </div>
    <div>
      <label>Start from:</label>
      <textarea v-model="startTime"></textarea>
      <label>End at:</label>
      <textarea v-model="endTime"></textarea>
    </div>
    <div>
      <label>Loop Count:</label>
      <textarea v-model="loopCount"></textarea>
    </div>
    <button @click="loopStart">loop start</button>
  </div>
</template>

<script>
import Vue from 'vue'
import VueYoutube from 'vue-youtube'
import getYouTubeID from 'get-youtube-id'

Vue.use(VueYoutube)

export default {
  data() {
    return {
      videoId: 'lG0Ys-2d4MA',
      playerVars:{
        start: 5,
        end: 10,
        loop: 1,
        rel: 0,
        playlist: 'lG0Ys-2d4MA'
      },
      newURL: undefined,
      playing: false,
      startTime: 0,
      endTime: 0,
      loopCount: 1
    }
  },
  methods: {
    playVideo() {
      this.player.playVideo()
      this.playing = true
    },
    pauseVideo() {
      this.player.pauseVideo()
      this.playing = false
    },
    playingVideo() {
      console.log('we are watching!!!')
    },
    async setLoop(){
      for (let n = this.loopCount; n > 0; n--) {
        this.player.seekTo(this.startTime)
        this.playVideo()
        await this.promiseBasedSetTimeout(() => { this.pauseVideo() }, (this.endTime - this.startTime + 1) * 1000 )
      }
      this.pauseVideo()
    },
    promiseBasedSetTimeout(resolve, interval) {
      return new Promise((resolve) => setTimeout(resolve, interval))
    },
    changeVideo() {
      this.videoId = getYouTubeID(this.newURL)
      return this.videoId
    },
    loopStart() {
      this.changeVideo()
      this.setLoop()
    }
  },
  computed: {
    player() {
      return this.$refs.youtube.player
    }
  }
}
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
