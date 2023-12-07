<template >
    <div class="box">
    <div class="content">
   <AppInfo :moviesLength="movies.length" :allfavoriteCount="movies.filter(c => c.favorite).length"/>
   <div class="search">
    <Search :UpdateTermHandle="UpdateTermHandle"/>
    <Filter :updateFilterHandler="updateFilterHandler" :filterName="filter"/>
   </div>

   <!-- Loading -->
     <div v-if="isLoading" class="text-center mt-5">
        <div  class="spinner-border  text-center" role="status">
       <span class="visually-hidden text-center">Loading...</span>
      </div>
     </div>

      <!-- Movies Not -->
     <div v-else-if="!movies.length" class="text-center mt-5 ">
        <h1 class="text-danger fw-bold">Kino Yo'q</h1>
    </div>

   <Movies v-else :movies="onFilterHandler(searchHandle(movies, term),filter)" @onremove="onremove" @onTogle="onTogle"/>
   <MovieAddForm @createForm="createForm"/>
    </div>
    </div>
</template>
<script>
import AppInfo from '../app-info/app-info.vue';
import Search from '../search/search.vue'
import Filter from '../filter/filter.vue'
import Movies from '../movies/movies.vue';
import MovieAddForm from '../movie-addForm/movie-addForm.vue';
import axios from 'axios'
export default {
  components: { AppInfo, Search, Filter, Movies, MovieAddForm },
//   Intial State Boshlang'ich qiymat 
  data() {
    return {
        movies:[
        ],
        term:"",
        filter:'all',
        isLoading:false
    }
  },
methods:{
   async createForm(item){
        try {
                const response = await axios.post('https://jsonplaceholder.typicode.com/posts', item)
                this.movies.push(response.data)
            } catch (error) {
                alert(error.message)
            }
    },
   async onremove(id){
    try {
        const data = await axios.delete(`https://jsonplaceholder.typicode.com/posts/${id}`)
        this.movies = this.movies.filter(c => c.id !== id)  
    } catch (error) {
        alert(error.message)
    }
    
 },

 onTogle({id,prop}){
   this.movies = this.movies.map(item => {
    if(item.id == id){
        return {...item,[prop]: !item[prop]}
    }

    return item
   })
 },
 searchHandle(arr,term){
    if(term.length == 0){
        return arr
    }

    return this.movies.filter(c => c.name.toLowerCase().indexOf(term) > -1)
 },
  onFilterHandler(arr, filter){
      switch (filter) {
        case 'popular':
        return  arr.filter(c => c.like == true)
        
        case 'mostviewrs':
            return arr.filter(c => c.viewrs > 500)
            
        default:
           return arr
      }
    },
 UpdateTermHandle(term){
   this.term = term
 },
 updateFilterHandler(filter) {
            this.filter = filter
},
async FetMovie(){
   try {
     this.isLoading = true
    const {data} = await axios.get('https://jsonplaceholder.typicode.com/posts',{
      params:{
        _limit:10
      }
    })
    const newArr = data.map(item => (
        {
            id:item.id,
            name:item.title,
            like:false,
            favorite:false,
            viewrs:item.id * 100
        }
    ))
    this.movies = newArr
    this.isLoading = false
   } catch (error) {
    alert(error.message)
   }
}
        
},
mounted() {
    this.FetMovie()
},

}
</script>
<style >
    .box{
        height: 100vh;
        background-color: #fff;
    }
    .content{
        height: 70vh;
        width: 70%;
        margin: 0 auto;
    }
    .search{
     background-color: #fff;
    border-radius: 5px;
    padding: 1.5rem;
    margin-top: 2rem;
    box-shadow: 15px 15px 15px 30px rgba(0, 0, 0, 0.15);
    }
</style>