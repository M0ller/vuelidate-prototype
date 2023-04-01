<template>
  <div class="divide">
    <div class="login">
    <h1>Login page</h1>
    
    <label for="username">Username</label>
    <input v-model="username" class="inputField">
    <p class="errorField" v-if="v$.username.$error">Name field has an error.</p>
      
      <div style="height: 50px"/>
    <label for="username">Email</label>
    <input v-model="email" class="inputField">
    <p class="errorField" v-if="v$.email.$error">Email field has an error.</p>
      
    <label for="username">Checkbox State: {{ checkBoxState }}</label>
      
    <input type="checkbox" value="State" v-model="checkBoxState" class="inputField">
    <p class="errorField" v-if="v$.checkBoxState.$error">State have a error.</p>
    
    <button
        class="inputField"
        @click="submitForm"
    >Submit
    </button>
  </div>
  <div class="login">
    <h1>Vuelidate states:</h1>
    <p>username: {{username}}</p>
    <p>v$.username.$error: {{v$.username.$error}}</p>
    <p>v$.username.$invalid: {{v$.username.$invalid}}</p>
    <p>v$.username.$dirty: {{v$.username.$dirty}}</p>
    <span>------------------------------------------</span>
    <div style="height: 20px"/>
    <p>email: {{email}}</p>
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
    <button
        class="inputField"
        @click="resetInputFields"
    >Reset Input Fields
    </button>
  </div>
    
    <div style="min-width: 250px">
    <p>Checkbox: {{checkBoxState}}</p>
    <p>v$.checkBoxState.$error: {{v$.checkBoxState.$error}}</p>
    <p>v$.checkBoxState.$invalid: {{v$.checkBoxState.$invalid}}</p>
    <p>v$.checkBoxState.$dirty: {{v$.checkBoxState.$dirty}}</p>
    <button @click="consoleLogProperties">Console.log properties</button>
    </div>
  </div>
  
</template>

<script>
import {useVuelidate} from '@vuelidate/core'
import {email, required} from '@vuelidate/validators'

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
      checkBoxState: null,
    }
  },
  validations() {
    return {
      username: {required},
      email: {required, email},
      checkBoxState: {required}
    }
  },
  methods: {
    async submitForm() {
      const isFormCorrect = await this.v$.$validate() // this sets the $dirty state
      if (isFormCorrect) {
        alert('Form is valid.')
      } else
        alert('Form has errors.')
    },
    resetDirty() {
      this.v$.username.$reset()
      this.v$.email.$reset()
      // or this.v$.$reset() // resets all validations
    },
    resetInputFields() {
      this.username = ''
      this.email = ''
      this.checkBoxState = null
    },
    consoleLogProperties(){
      console.log("username: ", this.username)
      console.log("email: ", this.email)
      console.log("CheckboxState: ", this.checkBoxState)
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

.errorField {
  color: red;
}

</style>
