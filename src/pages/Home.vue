<template>
    <a-form summary v-model="formValid">
      <template v-slot:summary="{ errors }">
        <h3>
          Custom Summary
        </h3>
        <div>
          <ul>
            <li v-for="error in errors" :key="'error-'+error+''">{{error}}</li>
          </ul>
        </div>
      </template>
     <a-input label="First Name" v-model="form.firstName" 
     :rules="firstNameRules" :textLimit="15"/>
     
     <a-input label="Last Name" v-model="form.lastName" 
     :rules="lastNameRules" :textLimit="15"/>
     
     <a-select
      label="Gender" 
      v-model="form.gender" 
      placeholder="Select your gender"
      :options="genderList"/>

      <a-select
      label="Age" 
      v-model="form.age" 
      placeholder="Select your age"
      :options="ageList"/>

      <a-textarea label="Bio"
      v-model="form.bio"
      :textLimit="255"
      resize="vertical"
      autoResize
      />

     <!-- <div>{{form}}</div> -->

     <a-sbutton :loading="loading"  @click="createProfile({ api: $api, form})" 
     :disabled="!formValid || loading">Create Profile</a-sbutton>
     <!-- <vue-editor v-model="content"></vue-editor>  -->
    </a-form>
</template>

<script>
//import { VueEditor } from "vue2-editor";
import { mapActions, mapState } from "vuex";

export default {
    // components: {
    //   VueEditor
    // },
    data(){
    return{
      firstNameRules:[
        v => v.length > 0 || "First name is required",
        v => !/\s/.test(v) || "No white spaces buddy"
      ],
      lastNameRules:[
        v => v.length > 0 || "Last name is required",
      ],
      form:{
      firstName: "",
      lastName: "",
      gender: "",
      age: "",
      bio: ""
      },
      //loading:false,
      formValid: false
    }
  },
  methods: {
    ...mapActions('profiles', {
      createProfile: 'CREATE_PROFILE'
    })
  //     createProfile(){
  //       this.loading = true;
  //      this.$api.post("Profile/", this.form).then(res => {
  //               //todo store result in vuex
  //               this.loading=false;
  //               this.$store.commit("ADD_PROFILE", res.data)
  //               //alert(res.data);
  //           }).catch(error => {
  //                   console.log(error.response)
  //             }); 
  //     }
  },
  computed:{
    ...mapState('profiles', {
        loading: state => state.creatingProfile
    }),
    fullName(){
      return this.form.firstName + " " + this.form.lastName;
    },
    genderList(){
      return[
        {value:"Male", text:"Male"},
        {value:"Female", text:"Female"},
        {value:"Other", text:"Other"}
      ];
    },
    ageList(){
      let result = [];
      for(let i=16; i<65; i++)
        result.push({value: i, text: i});
      return result;
    }
  }
  // beforeRouteEnter(to,from,next){
  //     //console.log("Route enter, fetch some data");
  //     let formString = localStorage.getItem('home-form') || null;
  //     next(vm => {
        
  //       if(formString !== null && formString !== "")
  //         vm.form = JSON.parse(formString);
  //     });
  // },
  // beforeRouteLeave(to,from,next){
  //     //console.log("route leave, save/cleanup state");
  //     let formString = JSON.stringify(this.form);
  //     localStorage.setItem('home-form', formString);
  //     next();
  // }
}

</script>

<style>

</style>
