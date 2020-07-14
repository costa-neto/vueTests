<template>
  <div id="app">
    <div>
      <!-- <a @click="page='home'">Home</a>
      <a @click="page='login'">Login</a> -->
    <router-link to="/">Home</router-link>
    <router-link to="/login">Login</router-link>
    <router-link to="/profile">Profile</router-link>
    </div>
    
    <router-view></router-view>
    
    <!-- <component :is="component"></component> -->
  </div>
</template>

<script>
// import Home from "./pages/Home"
// import Login from "./pages/Login"

export default {
  name: "App",
};
</script>

<style lang="stylus">
#app
  margin-top 60px

a
  padding 0 5px
</style>
