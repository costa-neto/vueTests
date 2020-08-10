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
import {mapGetters, mapActions} from 'vuex';

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
    watch: {
        profile: {
            immediate: true,
            handler(profile){
                if(profile !== undefined)
                this.setPopup("Selected Profile: "+profile.firstName);
            }
        }
    },
    methods: {
        ...mapActions('popup',{
            setPopup: 'DISPLAY_POPUP'
        })
    },
    computed: {
        ...mapGetters('profiles', {
            getProfile: 'GET_PROFILE'
        }),
        profile(){
            return this.getProfile(this.$route.params.name)
            
        }
    }
}
</script>

<style lang="stylus" scoped>

</style>