<template>
  <div class="login">
    <h1>This is a login page</h1>
  </div>

  <div>

    <labe>
      <input v-model="name">
      <div v-if="v$.name.$error"> Name field has an error.</div>
    </labe>
    
    <div>
      <label>Username</label>
      <br>
      <input
          v-model="username"
      >
    </div>
    <div>
      <label>Email</label>
      <br>
      <input
          type="text"
          v-model="email"
      >
    </div>
    <div>
      <label>Password</label>
      <br>
      <input
          type="text"
          v-model="password"
      >
    </div>
    <div>
      <label>Confirm Password</label>
      <br>
      <input
          type="text"
          v-model="confirmPassword"
      >
    </div>
  </div>

  <button
      @click="submitForm"
  >Submit
  </button>
</template>

<script>
import useVuelidate from "@vuelidate/core";
import {required} from "@vuelidate/validators";

export default {
  setup: ()=> ({ v$: useVuelidate() }),
  // setup() {
  //   return {
  //     v$: useVuelidate()
  //   }
  // },
  data() {
    return {
      name: "",
      username: "",
      email: "",
      password: "",
      confirmPassword: "",
    }
  },
  validations() {
    return {
      name: {required},
      username: {required},
      email: {required},
      password: {required},
      confirmPassword: {required},
    }
  },
  methods: {
    submitForm: async () => {
      const result = v$.$validate()
      if (result) {
        alert("Success!")
      } else {
        alert("Error!")
      }
    }
  }
}

</script>
<style scoped>

</style>