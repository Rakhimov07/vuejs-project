<template>
    <div class="movie-add-from">
        <h3 class="mb-4">Kino Qo`shing`</h3>
        <form class="add-form d-flex" @submit.prevent>
            <input type="text" class="form-control" placeholder="Qanday Kino ?" v-model="name">
            <input type="number" class="form-control" placeholder="Necha marotaba ko`rilgan" v-model="viewrs">
            <button class="btn-outline-dark" @click="submitHandler">Qo`shish`</button>
            </form>
    </div>
</template>
<script>
export default{
    data(){
        return{
            name: '',
            viewrs: ''
        }
    },
    methods:{
        submitHandler(){
            if(this.name == "" || this.viewrs == ""){
                return null
            }
         const obj = {
        name:this.name,
        viewrs:this.viewrs,
        like:false,
        favorite:false,
        id: Date.now()
       }
         this.name = '';
        this.viewrs = '';
         this.$emit('createForm',obj)
       
        }
    }
}
</script>
<style>
.movie-add-from{
    padding: 1.5rem;
    margin-top: 2rem;
    background-color: #fff;
    border-radius: 4px;
    box-shadow: 15px 15px 30px rgba(0, 0, 0, 0.15);
}
</style>