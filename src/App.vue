<template>
  <div id="app">
    <div class="header">
      <i class="fab fa-spotify"></i>
    </div>
    
    <div class="container">
      
      <Search 
      @ricerca='searching'
      />
      <GenreFilters 
      v-if="false"
      :possibleGenres= this.genreArray 
      @searchCurrentGenre='setGenre'
      />
      <div class="row">
        <Album 
        v-for="(music,index) in generalFilter"
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
import GenreFilters from '@/components/GenreFilters'

export default {
  name: 'App',
  data(){
    return{
      axios,
      musicArray:[],
      genreArray:[],
      textToSearch:'',
      filterValue:0,
      filterGenre:'0'
    }
  },
  methods:{
    searching(text,option){
      this.textToSearch=text;
      this.filterValue=option;
      console.log('app filter:',this.filterValue);
    },
    setGenre(genere){
      console.log('ricerca genere: ', genere);
      this.filterGenre = genere;
    }
  },


  components: {
    Album,
    Search,
    GenreFilters
  },
  created(){
    axios.get('https://flynn.boolean.careers/exercises/api/array/music')
    .then(res => {
      this.musicArray=res.data.response
      console.log(res.data.response)
      /* popolo possibili generi:  */
      for(let i=0;i<this.musicArray.length;i++){
        if(!this.genreArray.includes(this.musicArray[i].genre)){
          this.genreArray.push(this.musicArray[i].genre)
        }
      }
      console.log('generi: ',this.genreArray);
    })
    .catch(err => {
      console.error(err); 
    })
  },
  computed:{
    changeFilterType(){
      return this.filterByGenre;
    },
    generalFilter(){
      if(this.textToSearch==='') return this.musicArray
      if(this.filterValue===0) return this.musicArray.filter(item => item.genre.toLowerCase().includes(this.textToSearch.toLowerCase())) /* RICERCA PER GENERE COME DEFAULT */
      return this.musicArray.filter(item => item[this.filterValue].toLowerCase().includes(this.textToSearch.toLowerCase()))
      
    },
    filterByGenre(){
      console.log('current genre: ',this.filterGenre);
      if(this.filterGenre!=='0'){
        return this.musicArray.filter(item=>item.genre.toLowerCase()===this.filterGenre.toLowerCase())
      }
      return this.musicArray
    },
    filterByAuthor(){
      console.log('filter author');
      return 'author'
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
