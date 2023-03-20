<template>
  <div class="divide">
    <div class="login">
    <h1>Login page</h1>
    
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
  <div class="login">
    <h1>Vuelidate states:</h1>
    <p>v$.username.$error: {{v$.username.$error}}</p>
    <p>v$.username.$invalid: {{v$.username.$invalid}}</p>
    <p>v$.username.$dirty: {{v$.username.$dirty}}</p>
    
    <br>
    <p>isEmailValid: {{isEmailValid}}</p>
    <p>v$.email.$error: {{v$.email.$error}}</p>
    <p>v$.email.$invalid: {{v$.email.$invalid}}</p>
    <p>v$.email.$dirty: {{v$.email.$dirty}}</p>
    <br>
    <button
        class="inputField"
        @click="resetDirty"
    >Reset Dirty state
    </button>
  </div>
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
    },
    async resetDirty() {
      this.v$.username.$reset()
      this.v$.email.$reset()
    }
  },
  computed: {
    isEmailValid: {
      get() {
        return this.v$.email.$error
      }
    }
  }
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
  margin-bottom: 5px;
}

.divide {
  display: flex;
  flex-direction: row;
  column-gap: 20px;
}

</style>
