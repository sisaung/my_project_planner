<template>
  <!-- <h1>Edit {{id}}</h1> -->
  <form @submit.prevent="updateProject">
    <label>Title</label>
    <input type="text"  v-model="title" required/>

    <label>Details</label>
    <textarea cols="20" rows="10" v-model="detail" required></textarea>

    <button>Update Project</button>
  </form>
</template>

<script>
export default {
  props:['id'],
      data(){
          return{
            title:"",
            detail:"",
            api:"http://localhost:3000/projects/",
            e:null
          }
      },
      mounted(){
          fetch(this.api+this.id)
          .then((response)=>{
             return response.json()
          })
          .then((datas)=>[
              this.title = datas.title,
              this.detail = datas.detail
          ])
          .catch((err)=>{

          })
      },
      
      methods:{
        updateProject(){
          let updateRoute = this.api + this.id
            fetch(updateRoute,{
                method:'PUT',
                headers:{
                  "Content-Type": "application/json"
                },
                
                body:JSON.stringify(
                  {
                      title:this.title,
                      detail:this.detail
                  }
                )
            })
            .then(()=>{
                this.$router.push('/')
            })
            .catch((err)=>{
                console.log(err);
            })
        }
      }

}
</script>

<style>

</style>