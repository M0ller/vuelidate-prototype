<template>
  <div class="login">
    <h1>This is a login page</h1>
  </div>

  <div>

    <label>
      <input v-model="name">
      <div > Name field has an error.</div>
    </label>

    <div>
      <label>Username</label>
      <br>
      <input
          v-model="formData.username"
      >
    </div>
    <div>
      <label>Email</label>
      <br>
      <input
          type="text"
          v-model="formData.email"
      >
    </div>
    <div>
      <label>Password</label>
      <br>
      <input
          type="text"
          v-model="formData.password"
      >
    </div>
    <div>
      <label>Confirm Password</label>
      <br>
      <input
          type="text"
          v-model="formData.confirmPassword"
      >
    </div>
  </div>

  <button
      @click="submitForm"
  >Submit
  </button>
</template>

<script setup>
import useVuelidate from "@vuelidate/core";
import {required} from "@vuelidate/validators";
import {reactive} from "vue";

const formData = reactive({
  name: "",
  username: "",
  email: "",
  password: "",
  confirmPassword: "",
});

const rules = {
  name: {required},
  username: {required},
  email: {required},
  password: {required},
  confirmPassword: {required},
};

const v$ = useVuelidate(rules, formData);
const submitForm = async () => {
  const result = await v$.value.validate;
  if (result) {
    alert("Success!")
  } else {
    alert("Failed!")
  }
}


</script>
<style scoped>

</style>