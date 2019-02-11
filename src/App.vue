<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">City</router-link>
      <router-link to="/artist">Artist</router-link>
    </div>
    <router-view/>
  </div>
</template>

<style lang="scss">
body{
  margin:0;
  padding:0;
  box-sizing: border-box;
}
#app {
  font-family: Montserrat, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
#nav {
  padding: 30px;
  a {
    font-weight: 400;
    color: white;
    margin:120px 5px;
    font-size:25px;
    text-decoration: none;
    background-color: #1976D2;
    padding:10px 35px;
    border-radius:7px;
    &.router-link-exact-active {
      color: white;
    }
  }
}
</style>
