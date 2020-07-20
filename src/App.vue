<template>
  <div id="app">
    <div>
      <!-- <a @click="page='home'">Home</a>
      <a @click="page='login'">Login</a> -->
    <router-link to="/">Home</router-link>
    <router-link to="/login">Login</router-link>
    <router-link to="/profile">Profile</router-link>
    </div>
    
    <div class="app">
      <div class="main">
        <router-view></router-view>
      </div>
      <div class="menu">
          <router-link v-for="p in profiles"
           :to="'/profile/'+p.firstName+''"
           :key="p.Id">
                {{p.firstName}} - {{p.lastName}}
          </router-link>
      </div>
    </div>
    <!-- <component :is="component"></component> -->
  </div>
</template>

<script>
// import Home from "./pages/Home"
// import Login from "./pages/Login"

export default {
  name: "App",
  created(){
      this.$store.dispatch("LOAD_PROFILES",this.$api);
      // this.$eventBus.$on('created-profile', (data) => {
      //   this.profiles.push(data);
      // })
  },
  computed: {
    profiles() {
      return this.$store.getters.GET_PROFILES;
    }
  }
  
};
</script>

<style lang="stylus">
#app
  margin-top 60px

a
  padding 0 5px

.app
  display flex
  flex-direction row

</style>
