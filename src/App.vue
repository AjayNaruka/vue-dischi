<template>
  <div id="app">
    <div class="header">
      <i class="fab fa-spotify"></i>
    </div>
    
    <div class="container">
      <Search 
      @ricerca='searching'
      />
      <div class="row">
        <Album 
        v-for="(music,index) in filterAlbums"
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
import Search from '@/components/Search'

export default {
  name: 'App',
  data(){
    return{
      axios,
      musicArray:[],
      textToSearch:'',
      filterValue:0
    }
  },
  methods:{
    searching(text,option){
      this.textToSearch=text;
      this.filterValue=option;
      console.log('app filter:',this.filterValue);
    }
  },


  components: {
    Album,
    Search
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
  },
  computed:{
    filterAlbums(){
      if(this.textToSearch==='') return this.musicArray
      if(this.filterValue===0) return this.musicArray.filter(item => item.genre.toLowerCase().includes(this.textToSearch.toLowerCase()))
      return this.musicArray.filter(item => item[this.filterValue].toLowerCase().includes(this.textToSearch.toLowerCase()))
    }
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
