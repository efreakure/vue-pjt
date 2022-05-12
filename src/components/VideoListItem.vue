<template>
  <div>
    <li @click="selectVideo" class>
      <img :src="videoUrl" alt="image">
      {{ videoTitle }}
    </li>
    <hr>
    <br>
  </div>
</template>

<script>
import _ from 'lodash'

// npm i lodash

export default {
  name: 'VideoListItem',
  props:{
    videoItem: {
      type: Object,
      required: true
    }
    
  },
  methods:{
    selectVideo(){
      this.$emit('select-video', this.videoItem)
    }
  },
  computed:{
    videoTitle(){
      const title = _.unescape(this.videoItem.snippet.title)
      return title
    },
    videoUrl(){
      return this.videoItem.snippet.thumbnails.default.url
    }
  }
}
</script>

<style>

</style>