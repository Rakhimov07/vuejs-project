<template >
    <div class="app-info">
      <h3 class="fs-3">Barcha Kinolar : {{ moviesLength }}</h3>  
       <h3 class="fs-4">Ko'rilgan Kinolar : {{ allfavoriteCount }}</h3>
     </div>
</template>
<script>

export default {
    props:{
      moviesLength:{
        type:Number,
        required:true
      },
      allfavoriteCount:{
        type:Number,
        required:true
      }
    }
}
</script>
<style >
   .app-info{
    background-color: #fff;
    border-radius: 5px;
    padding: 1.5rem;
    margin-top: 2rem;
    box-shadow: 15px 15px 15px 30px rgba(0, 0, 0, 0.15);
    
   } 
</style>