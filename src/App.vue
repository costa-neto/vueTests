<template>
  <div id="app">
    <div>
      <a @click="page='home'">Home</a>
      <a @click="page='login'">Login</a>
    </div>

    <component :is="component"></component>
  </div>
</template>

<script>
import Home from "./pages/Home"
import Login from "./pages/Login"

export default {
  name: "App",
  data(){
    return{
      page: "home",
    };
  },
  components: {
    Home,
    Login
  },
  computed:{
    component() {
      if(this.page === "home") return Home;
      else if(this.page === "login") return Login;
      else {return Home;}
    }
  }
};
</script>

<style lang="stylus">
#app
  margin-top 60px


</style>
