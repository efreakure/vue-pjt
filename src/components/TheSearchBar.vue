<template>
  <div>
    <div 
      class="search-bar" 
      :style="{ margin: videosLength ? '0' : '40vh 0' }"
    >
      <input type="text" @keyup.enter="onInputKeyword" id="input">
      <button @click="onInputKeyword">검색</button>
    </div>
  </div>
</template>

<script>


export default {
  name: 'TheSearchBar',
  methods:{
    onInputKeyword(){
      const input = document.querySelector('#input')
      // this.$emit('input-change', event.target.value)
      this.$emit('input-change', input.value)
    }
  },
  props: {
    videosLength: Number
  },
}
</script>

<style>
.search-bar {
  transition-duration: 1s;
}
</style>