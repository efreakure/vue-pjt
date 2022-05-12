<template>
  <div>
    <ul>
      <video-list-item
        v-for="video in videos"
        :key="video.id.videoId"
        :video-item="video"
        @select-video="onSelectVideo"
      ></video-list-item>
    </ul>
  </div>
</template>

<script>

import VideoListItem from '@/components/VideoListItem.vue'
// import VideoListItem from './VideoListItem.vue'

export default {
  name:'VideoList',
  components:{
    VideoListItem
  },
  props:{
    videos: Array
  },
  methods: {
    onSelectVideo(video){
      this.$emit('select-video',video)
    }
  }

}
</script>

<style>

</style>