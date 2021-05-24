<template>
    <div class="album col-md-6 col-lg-2">
      <div class="album-container">
        <img class="img-fluid" :src="item.poster" alt="">
      <h4 class="white">{{item.title.toUpperCase()}}</h4>
      <h6>{{item.author}}</h6>
      <h6>{{item.year}}</h6>
      </div>
      
    </div>
</template>

<script>
export default {
name:'Album',
props:{
  item: Object
}
}
</script>

<style lang="scss" scoped>
  .album{
    display: flex;
    flex-direction: column;
    /* background: red; */
    .album-container{
      background: #2E3A46;
      text-align: center;
      min-height: 380px;
      margin-bottom: 10px;
      padding:5px 10px ;
      color: grey;
      img{
        margin-top:10px ;
      }
      h4.white{
        margin-top: 10px;
        color: white;
      }
    }
  }
  
  
</style>