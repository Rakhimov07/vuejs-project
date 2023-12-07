<template>
    <div class="btn-group">
         <button class="btn mt-2 " v-for="btn in filterButtons" 
         @click="filterHandler(btn.name)"
         :class="[filterName === btn.name ? 'btn-dark' : 'btn-outline-dark']">
          {{ btn.title }}  
         </button>
        </div>
</template>
<script>
export default {
    data() {
        return {
            filterButtons: [
                {
                    title: 'Barcha kinolar',
                    name: 'all'
                },
                {
                    title: 'Mashhur kinolar',
                    name: 'popular'
                },
                {
                    title: 'Eng kop kinolar',
                    name: 'mostviewrs'
                }
            ],
             filter: 'all',
        }},
       
    props: {
        updateFilterHandler: {
            type: Function,
            required: true
        },
        filterName: {
            type: String,
            required: true
        }
    },
    methods: {
        filterHandler(filter) {
            this.filter = filter
            this.updateFilterHandler(this.filter)
        }
    },

}
</script>
<style>
    
</style>