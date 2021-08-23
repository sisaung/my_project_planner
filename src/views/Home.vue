<template>
  <div class="home">
     
     <div>
          <FilterNav @filterNav="current = $event" :current="current"></FilterNav>
      </div>

      <div v-for="project in filteredProjects" :key="project.id">
          <SingleProject  :project="project" @delete="deleteProject" @complete="completeDoneProject"></SingleProject>
      </div>

  </div>
</template>

<script>
import FilterNav from '../components/FilterNav'
import SingleProject from '../components/SingleProject'

// @ is an alias to /src

export default {
  name: 'Home',
  components: {
    FilterNav,
    SingleProject,
    
  },
    data(){
      return{
          projects:[], //{}{}{}
          current:"all",
      }
    },
    methods:{
      deleteProject(id){
          this.projects = this.projects.filter((project)=>{
              return project.id != id //{}
          })
      },
      completeDoneProject(id){
        let findCompleteProject = this.projects.find((project)=>{
            return project.id === id
        })
          findCompleteProject.complete = !findCompleteProject.complete
      },
      
    },
    computed:{
        filteredProjects() {
            if(this.current === 'complete') {
                return this.projects.filter((project)=> {
                    return project.complete
                })
            }
             if(this.current === 'ongoing') {
                return this.projects.filter((project)=> {
                    return !project.complete
                })
            }
            return this.projects
        } 
    },
  mounted(){
    fetch('http://localhost:3000/projects')
    .then((response)=>{
        return response.json()
    })
    .then((datas)=>{
        this.projects = datas
    })
    .catch((err)=>{
        console.log(err);
    })
  }
}
</script>
<style>
    
</style>