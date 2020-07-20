<template>
    <div v-if="profile">
        <h1> {{profile.firstName}} - {{profile.lastName}} Profile </h1>

        <div>
            <router-view></router-view>
        </div>
        <div>
              
               {{profile.age}} - {{profile.gender}} - {{profile.bio}}
        </div>
        <div>

        </div>
    </div>    
</template>

<script>

export default {
    // data(){
    //     return {
    //         profile: {}
    //     };
    // },
    // watch:{
    //     "$route.params.name": {
    //         immediate: true,
    //         handler(name){
    //             this.loadProfile(name)
    //         }
    //     }
    // },
    // methods: {
    //     loadProfile(name){
            
    //         this.$api.get("Profile/"+name).then(res => {
    //                 this.profile = res.data;
    //             });
    //     }
    // },
    computed: {
        profile(){
            let profiles = this.$store.getters.GET_PROFILES;
            if(profiles.length <= 0) return null;
            let name = this.$route.params.name;
            return profiles.filter(
                x => x.firstName === name)[0];
        }
    }
}
</script>

<style lang="stylus" scoped>

</style>