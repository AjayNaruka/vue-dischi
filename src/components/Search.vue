<template>
  <form class="d-flex">
    <div class="flex-grow-1">
      <input
        class="form-control"
        placeholder="Cerca"
        v-model.trim=inputText
        type="text">
    </div>
    <div>
      <select name="filters" id="filters" class="my-select" @change="optionChange($event)">
        <option v-if="searchOnce" >--scegli--</option>
        <option value="genre">Genere</option>
        <option value="author">Artista</option>
        <option value="year">Anno</option>
      </select>
      <button class="ms-3 btn btn-primary" @click.prevent="startSearch()">CERCA</button> <!-- PREVENT per evitare il reload della pagina dovuto dal form -->
      <button class="ms-3 btn btn-warning" @click.prevent='resetSearch()'>RESET</button>
      <!-- <label for="filters"></label> -->
      
    </div>
  </form>
</template>

<script>
export default {
  name:'Search',
  data(){
    return{
      searchOnce:true,
      inputText:'',
      /* filterOption:this.optionChange() */
      filterOption:0,
    }
  },
  methods:{
    resetSearch(){
      console.log('reset');
      this.inputText='';
      this.startSearch();
    },
    startSearch(){
      this.$emit('ricerca',this.inputText,this.filterOption)
    },
    optionChange(event){
      this.searchOnce=false
      console.log(event.target.value);
      this.filterOption=event.target.value
      console.log('option: ', this.filterOption);
      return event.target.value
    }
  },
  
}
</script>

<style>
form{
  margin-bottom: 15px ;
}
  input{
    margin-bottom: 20px;
  }
  .my-select{
    vertical-align: middle;
   padding: 7px;
   margin-left: 10px ;
   border-radius: 5px;
  }
</style>