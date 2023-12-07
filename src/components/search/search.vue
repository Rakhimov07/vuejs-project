<template>
      <input type="text"
         placeholder="Kino qidrish"
          class="form-control"
         @input="onHandle">

</template>
<script>
export default {
      props:{
            UpdateTermHandle:{
                  type:Function,
                  required:true
            }
      },
   data() {
      return {
            term:''
      }
   }, 
   methods: {
      onHandle(e){
            this.term = e.target.value
            this.UpdateTermHandle(this.term)
      }
   },
}
</script>
<style>
    
</style>