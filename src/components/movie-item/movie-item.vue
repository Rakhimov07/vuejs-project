<template>
   <li class="d-flex  list-group-item justify-content-between align-items-center"
   :class="[{like:movie.like},{favorite:movie.favorite}]">
    <span @click="$emit('onTogle',{id: movie.id, prop:'like'})" class="name form-label">{{ movie.name }}</span>
     <input type="number" :value="movie.viewrs" class="form-input">
     <div class="buttons flex justify-space-between align-items-center">
        <button class="cookies"  @click="$emit('onTogle',{id: movie.id, prop:'favorite'})"><i class="fa-solid fa-cookie"></i></button>
        <button class="trash" @click="$emit('onremove',movie.id)"><i class="fa-solid fa-trash"></i></button>
        <i class="fa-solid fa-star"></i>
     </div>
   </li>
</template>
<script>
export default {
    props:{
      movie:{
        type:Object,
        required:true
      },
    },

}
</script>
<style>
  .name{
    width: 800px;
    font-size: 24px;
    font-weight: bold;
    cursor: pointer;
    line-height: 27px;

  }  
  input{
    outline-color: beige;
    padding: 8px;
    width: 70px;
    border: none;
  }
  .cookies{
    line-height: 27px;
    width: 38px;
    height: 37px;
    color: rgb(206, 206, 30);
  }
  .trash{
    line-height: 27px;
    width: 38px;
    height: 37px;
    margin-left: 10px;
    color: red;
  }
  .fa-star{
    opacity: 0;
    transform: translateX(30px);
    line-height: 27px;
    padding-top: 10px;
    font-size: 20px;
    color: rgb(197, 197, 47);
    width:50px;
    height: 50px;
    text-align: center; 
  }
    
    .buttons{
      display: flex;
      align-items: center;
    }
     .list-group-item.like .fa-star{
    opacity: 1;
    transform: translateX(0px);
    transition:  all .7s ease;
   }
   .list-group-item.favorite .form-label{
    color: rgb(201, 166, 26);
   }
   .list-group-item.favorite .form-input{
    color: rgb(201, 166, 26);
   }

</style>