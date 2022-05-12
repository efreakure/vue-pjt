<template>
  <div id="app">
    <h1>Youtube</h1>
    <header>
      <the-search-bar
        @input-change="onInputChange"
        :videos-length="videosLength">
        :videos-length="videos.length">
      ></the-search-bar>
    </header>

    <!-- {{ selectedVideo }} -->
    <section>
      <video-detail :selected-video="selectedVideo"></video-detail>
      <video-list :videos="videos" @select-video="onSelectVideo"></video-list>
    </section>
  </div>
</template>

<script>
console.log(process.env.VUE_APP_HAHA, 'why...')
const API_URL = 'https://www.googleapis.com/youtube/v3/search'
const API_KEY = process.env.VUE_APP_YOUTUBE_API_KEY

import axios from 'axios'

import TheSearchBar from '@/components/TheSearchBar.vue'
import VideoList from '@/components/VideoList.vue'
import VideoDetail from '@/components/VideoDetail.vue'


export default {
  name: 'App',
  components: {
    TheSearchBar,
    VideoList,
    VideoDetail,
  },
  data(){
    return {
      inputValue: null,
      videos:[],
      selectedVideo: null,
    }
  },
  methods:{
    onInputChange(data){
      this.inputValue = data

      const params = {
          key: API_KEY,
          part: 'snippet',
          type: 'video',
          q: this.inputValue,
        }

      axios({
        method: 'get',
        url: API_URL,
        params
      })
        .then(res =>{
          this.videos = res.data.items
          this.selectedVideo = this.videos[0]
        })
        .catch(err => {
          console.log(err)
        })

    },
    onSelectVideo(video){
      this.selectedVideo = video
      console.log(video)
    }
  },
  computed:{
    videosLength(){
      return this.videos.length
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
section {
  display: flex
}
</style>
