<script setup>
import { reactive } from 'vue'
import { useVuelidate } from '@vuelidate/core'
import { email, required, minLength } from '@vuelidate/validators'
import { useRouter } from 'vue-router'

const router = useRouter()

const state = reactive({
  email: '',
  password: ''
})

const rules = {
  email: { required, email },
  password: { required, minLength: minLength(6)  },
}

const v$ = useVuelidate(rules, state)

const submit = () => {
  v$.value.$validate()
  !v$.value.$error ? console.log("submit") : console.log("nosubmit")
  if (!v$.value.$error) {
    router.push({ name: "game"})
  }
}
</script>

<template>
  <v-card>
    <form @submit.prevent="submit">
      <div style="padding: 4rem">
        <v-text-field
          v-model="state.email"
          :error-messages="v$.email.$errors.map(e => e.$message)"
          @input="v$.email.$touch"
          @blur="v$.email.$touch"
          label="Email"
          required
          style="width: 300px"
        ></v-text-field>
        <v-text-field
          v-model="state.password"
          :error-messages="v$.password.$errors.map(e => e.$message)"
          @input="v$.password.$touch"
          @blur="v$.password.$touch"
          label="Password"
          required
        ></v-text-field>
        <v-btn
          class="me-4"
          @click="submit"
        >
          submit
        </v-btn>
      </div>
    </form>
  </v-card>
</template>
