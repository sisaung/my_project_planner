<template>
  <form @submit.prevent="addProject">
    <label>Title</label>
    <input type="text" v-model="title" required/>

    <label>Details</label>
    <textarea cols="20" rows="10" v-model="detail" required></textarea>

    <button>Add Project</button>
  </form>
</template>

<script>
export default{
      data(){
            return{
                  title:"",
                  detail:""
            }
      },
      
      methods:{
            addProject(){
                  fetch("http://localhost:3000/projects/",{
                        method:'POST',
                        headers:{
                              'Content-Type': 'application/json'
                        },
                        body:JSON.stringify(
                              {
                                    title:this.title,
                                    detail:this.detail,
                                    complete:false
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

};
</script>

<style>
form {
      background-color: #f2f2f2;
      max-width: 500px;
      padding: 20px;
      margin: 10px auto;
      border-radius: 10px;
      box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px;
}
label {
      display: block;
      text-align: left;
      padding: 2px;
      margin: 8px;
      letter-spacing: 1px;
      text-transform: uppercase;
      font-weight: bold;
      font-size: 0.9em;
      color:#777;
}
input {
      padding: 10px;
      width: 96%;
      border: 0;
      border-bottom: 1px solid #777;
      outline: none;

}
input:focus{
      background-color: rgb(207, 200, 200);
      transition: 0.6s;
}

form button {
      margin: 20px;
      padding: 16px;
      background: #42b983;
      border: none;
      color: white;
      border-radius: 10px;
      cursor: pointer;
      box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px;
}
textarea {
      width: 446px;
      border-color:rgb(180, 180, 180);
      outline: none;

}
textarea:focus{
      background-color: rgb(207, 200, 200);
      transition: 0.6s
}

button:hover {
      background-color: #39a373;
      transition: 1s;
}
</style>