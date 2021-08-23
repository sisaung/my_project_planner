<template>
     <div class="project" :class="{complete:project.complete}">
         <div class="flexing">
             <div>
                 <h3 @click="showDetail =!showDetail">{{project.title}}</h3>
             </div>
                 
            <div>
                <span class="material-icons delete" @click="deleteProject">delete</span>
                <router-link :to="{ name:'EditProject',params:{ id:project.id }}">
                    <span class="material-icons edit">edit</span>
                </router-link>
                <span class="material-icons done" @click="completeProject">done</span>
            </div>
            
         </div>
         <p v-if="showDetail">{{project.detail}}</p>
         
         
     </div>

</template>

<script>
export default {
    props:['project'],
    data(){
        return{
            showDetail:false,
            api:"http://localhost:3000/projects/"
        }
    },
    methods:{
        deleteProject(){
            let deleteRoute = this.api+this.project.id
            fetch(deleteRoute,{method:'DELETE'})
            .then(()=>[
                this.$emit("delete",this.project.id)
            ])
            .catch((err)=>{
                console.log(err);
            })
        },
        completeProject(){
            let completeRoute = this.api + this.project.id
            fetch(completeRoute,
            {
                method:'PATCH',
                headers:{
                    'Content-Type':'application/json'
                },
                body:JSON.stringify(
                    {
                        complete:!this.project.complete 
                        //false =!false (true)
                    }
                )
            })
            .then(()=>{
                this.$emit("complete",this.project.id)
            })
            .catch((err)=>{
                console.log(err);
            })
            
        },
        
    }
}
</script>

<style>
    .project{
        background-color: #f2f2f2;
        padding: 25px 30px;
        text-align: left;
        margin: 25px;
        border-left: 5px solid crimson; 
        border-radius: 5px;
        box-shadow: rgba(25, 25, 25, .04)0 0 1px 0, rgba(0,0,0,.1) 0 3px 4px ;
    }
    h3{
        color:blueviolet;
        cursor: pointer;
        font-size: 1.1em;
    }
    .flexing{
        display: flex;
        justify-content: space-between;
        align-items: center;
    }
    
    span{
        padding-left: 8px;
        cursor: pointer;
    }
 
    .delete:hover{
        color:crimson;
    }
    .edit{
        color: #444
    }
    .edit:hover{
        color:#777;
    }
    .done:hover{
        color:#777;
    }
    
    .complete{
        border-left-color:#42b983;
    }
    .complete .done{
        color:#42b983;
        font-weight: bold;
        font-size: 1.7em;
    }
</style>    