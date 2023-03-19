<template>
  <div class="login">
    <h1>This is a login page</h1>
  </div>
  
  <div>
    <BaseInput 
        label="Username"
        v-model="username" 
        type="text"/>
    <BaseInput 
        label="Email"
        v-model="email" 
        type="text"/>
    <BaseInput 
        label="Password"
        v-model="password" 
        type="text"/>
    <BaseInput 
        label="Confirm Password"
        v-model="confirmPassword" 
        type="text"/>
    
<!--    <BaseInput -->
<!--        label="First Name" -->
<!--        v-model="firstName" -->
<!--        type="text"/>-->
<!--    <p>{{firstName}}</p>-->
  </div>
  
  <button
      @click="submitForm"
  >Submit</button>
</template>

<script setup>
import BaseInput from "@/components/BaseInput.vue"
import {reactive} from 'vue'
import {required} from "@vuelidate/validators";
import useVuelidate from "@vuelidate/core";

// const firstName = ref('')
const formData = reactive({
  username: "",
  email: "",
  password: "",
  confirmPassword: "",
})

const rules = {
  username: { required },
  email: { required },
  password: { required },
  confirmPassword: { required },
}

const v$ = useVuelidate(rules, formData)
const submitForm = async () => {
  const result = await v$.value.$validate()
  if (result) {
  alert("Success!")
  }else{
    alert("Error!")
  }
}

</script >
<style scoped>

</style>