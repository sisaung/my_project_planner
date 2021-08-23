<template>
  <div id="nav">

    <div class="main-nav">
      <router-link to="/">Projects</router-link>
      <router-link :to="{ name: 'AddProject' }">Add a New Project</router-link>
    </div>
  </div>
  <router-view />
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  max-width: 600px;
  margin: 0px auto;
  color: #2c3e50;
}
*{
  padding: 0px;
   margin:0px;
   box-sizing: border-box;
}
.main-nav {
    padding:15px;
    margin:30px;

}
.main-nav a{
    padding:10px;
    letter-spacing: 1px;
    text-decoration: none;
    color:#777;
    /* font-weight: bold; */
}

#nav a.router-link-exact-active {
    border-bottom: 2px solid #42b983;
    margin-bottom: 15px;
    
}
</style>
