<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}

.form{
  width:400px;
  margin:0 auto;
  text-align:center;
  padding-top:5rem;
}
*{
  border-radius:1px!important;
  box-sizing: border-box;
  margin:0;
  padding:0;
}
.flex{
  display: flex;
}
.between{
  display:flex;
  justify-content: space-between;
}
.center{
  display: flex;
  align-items: center;
}
.justify-center{
  display:flex;
  justify-content: center;
}
</style>
