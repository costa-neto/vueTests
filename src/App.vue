<template>
  <div id="app">
    <div class="loader" v-if="!ready">Loading</div>
    <PopUp />
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
import PopUp from './components/PopUp'
import {mapActions, mapState} from "vuex";


export default {
  name: "App",
  components:{
    PopUp
  },
  created(){
      this.init();
      this.loadProfiles(this.$api);
      //this.$store.dispatch("LOAD_PROFILES",this.$api);
      // this.$eventBus.$on('created-profile', (data) => {
      //   this.profiles.push(data);
      // })
  },
  methods:{
    ...mapActions({
      init: 'INIT_APP'
    }),
      ...mapActions('profiles',{
        loadProfiles:'LOAD_PROFILES'
  })
  },
  computed: {
    ...mapState({
      ready:"appReady"
    }),
    ...mapState('profiles',{
      profiles: state=> state.profiles

    })
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

.loader
  background #eee
  position fixed
  width 100%
  height 100%
  top 0
  left 0
</style>
