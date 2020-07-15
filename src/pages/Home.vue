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

     <div>{{form}}</div>

     <button v-if="formValid" @click="createProfile">Submit</button>
     <span v-else>Please fill out the form</span>
    </a-form>
</template>

<script>

export default {
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
      formValid: true
    }
  },
  methods: {
      createProfile(){
        this.$api.post("Profile/", this.form).then(res => {
                //todo store result in vuex
                alert(res.data);
            }).catch(error => {
                    console.log(error.response)
              });
      }
  },
  computed:{
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
  },
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
