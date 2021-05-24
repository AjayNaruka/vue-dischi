<template>
  <div id="app">
    <div class="header">
      <i class="fab fa-spotify"></i>
    </div>
    <div class="container">
      <div class="row">
        <Album 
        v-for="(music,index) in musicArray"
        :key="index"
        :item=music
        />
      </div>
    </div>
  </div>
</template>

<script>

import axios from 'axios'
import Album from '@/components/Album'

export default {
  name: 'App',
  data(){
    return{
      axios,
      musicArray:[]
    }
  },


  components: {
    Album
  },
  created(){
    axios.get('https://flynn.boolean.careers/exercises/api/array/music')
    .then(res => {
      this.musicArray=res.data.response
      console.log(res.data.response)
    })
    .catch(err => {
      console.error(err); 
    })
  }
}
</script>

<style lang="scss">
@import '@/assets/styles/general';
body{
  background-color:#1E2D3B ;
}
body .header{
  background-color: #2E3A46;
  height: 70px;
  margin-bottom: 20px;
  i{
    line-height: 70px;
    font-size: 38px;
    margin-left: 10px;
    color: white;
    
  }
}
</style>
