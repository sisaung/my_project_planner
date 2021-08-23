<template>
   <div class="navbar">
         <div class="flex" >
              <div class="view-nav" @click="filterNavProject('all')" :class="{ active:current === 'all'}">view all</div>
              <div class="complete-nav" @click="filterNavProject('complete')" :class="{ active:current === 'complete'}">complete</div>
              <div class="ongoing-nav" @click="filterNavProject('ongoing')" :class="{ active:current === 'ongoing'}">ongoing</div>
         </div>
     </div>
</template>

<script>
export default {
    props:['current'],
        methods:{
                filterNavProject(value){
                        console.log(value);
                        this.$emit("filterNav",value)
                }
        }
}

</script>

<style>
    .navbar{
            margin-right:10px;
            width: 45%;
    }
    .flex{
            display: flex;
            justify-content: space-around;
            align-items: center;
            margin: 10px;
    }
    .view-nav{
            margin-left:20px;
            cursor: pointer;
            letter-spacing: 1px;
            color: #777;
            text-transform: uppercase;
            font-size: 0.7em;
            font-weight: bold;
            
    }
    

    .complete-nav{
            margin-left:15px;
            cursor: pointer;
            letter-spacing: 1px;
            color: #777;
            text-transform: uppercase;
            font-size: 0.7em;
            font-weight: bold;

    }
    
    .ongoing-nav{
            margin-left:15px;
            cursor: pointer;
            letter-spacing: 1px;
            color: #777;
            text-transform: uppercase;
            font-size: 0.7em;
            font-weight: bold;
    }
    .active {
            color: #333;
            
    }
    

</style>