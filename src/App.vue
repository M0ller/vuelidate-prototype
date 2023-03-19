<template>
  <div class="login">
    <h1>This is a login page</h1>
    
    <label for="username">Username</label>
    <input v-model="username" class="inputField">
    <p v-if="v$.username.$error">Name field has an error.</p>

    <label for="username">Email</label>
    <input v-model="email" class="inputField">
    <p v-if="v$.email.$error">Email field has an error.</p>
    
    <button
        class="inputField"
        @click="submitForm"
    >Submit
    </button>
  </div>
</template>

<script>
import {useVuelidate} from '@vuelidate/core'
import {required} from '@vuelidate/validators'

export default {
  setup() {
    return {
      v$: useVuelidate(),
    }
  },
  data() {
    return {
      username: '',
      email: '',
    }
  },
  validations() {
    return {
      username: {required},
      email: {required},
    }
  },
  methods: {
    async submitForm() {
      const isFormCorrect = await this.v$.$validate()
      if (isFormCorrect) {
        alert('Form is valid.')
      } else
        alert('Form has errors.')
    }
  },
}
</script>

<style scoped>

.login {
  display: flex;
  flex-direction: column;
  row-gap: 5px;
}

.inputField {
  width: 200px;
}

</style>
