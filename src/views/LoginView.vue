<template>
  <div class="login">
    <h1>This is a login page</h1>
  </div>

  <div>
    
    <input v-model="name">
    <p v-if="v$.name.$error">Name field has an error.</p>
    
  </div>

  <button
      @click="submitForm"
  >Submit
  </button>
</template>

<script>

import {useVuelidate} from '@vuelidate/core'
import {required} from '@vuelidate/validators'

export default {
  
  data() {
    return {
      v$: useVuelidate(),
      name: ''
    }
  },
  validations() {
    return {
      name: {required}
    }
  },
  methods: {
    submitForm() {
      this.v$.$touch()
      if (!this.v$.$error) {
        alert('Form is valid.')
      } else
      alert('Form has errors.')
    }
  },
}
</script>
<style scoped>

</style>