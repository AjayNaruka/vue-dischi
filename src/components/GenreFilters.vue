<template>
  <div>
    <select name="filter" id="genreFilter" @change="genreChange($event)">
      <option value="0">ALL</option>
      <option 
      v-for="(genere,index) in possibleGenres"
      :key="index"
      :value="genere.toLowerCase()"
      @click='startSearchGenre'
      >

      {{genere}}

      </option>
    </select>
  </div>
</template>

<script>
export default {
  name:'GenreFilters',
  data(){
    return{
      toSearchGenre:0,
    }
  },
  props:{
    possibleGenres:Array,
  },
  methods:{
    genreChange(event){
      this.toSearchGenre=event.target.value;
      console.log(this.toSearchGenre);
      this.$emit('searchCurrentGenre', this.toSearchGenre)
    },
    
  }
}
</script>

<style>
 #genreFilter{
   margin-bottom:20px
 }
</style>