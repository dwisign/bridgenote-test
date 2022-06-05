<template>
    <b-container>
        <b-form @submit.stop.prevent="submitEmail">
          <p class="small text-center mt-3">Enter your email below and we will send you reset password link to your email</p>

          <b-form-group id="email-input">
              <b-form-input
              placeholder="Email" 
              class="form-control"
              v-model="$v.forgot_password.email_input.$model"
              :state="validateState('email_input')"
              aria-describedby="email-input-feedback"
              ></b-form-input>

              <b-form-invalid-feedback id="email-input-feedback" v-if="!$v.forgot_password.email_input.required">Email is a required.</b-form-invalid-feedback>
              <b-form-invalid-feedback id="email-input-feedback" v-if="!$v.forgot_password.email_input.email">Please use valid format email address.</b-form-invalid-feedback>
          </b-form-group>
          <div class="mb-5 mt-4 text-center">
              <b-button 
                variant="primary" 
                size="lg" 
                type="submit"
              >
                Submit
              </b-button>
          </div>

          <div class="mb-3">
              <p class="text-center">
                  <NuxtLink to="/">Sign In</NuxtLink>
              </p>
          </div>
        </b-form>
    </b-container>
</template>

<script>
import { validationMixin } from "vuelidate";
import { required, email } from 'vuelidate/lib/validators'
export default {
  layout: 'user-access',
  mixins: [validationMixin],
  data() {
    return {
      forgot_password: {
        email_input: '',
      }
    }
  },
  validations: {
      forgot_password: {
            email_input: {
                required,
                email
            }
      }
  },
  methods: {
    validateState(email_input) {
        const { $dirty, $error } = this.$v.forgot_password[email_input];
        return $dirty ? !$error : null;
    },
    submitEmail() {
        this.$v.forgot_password.$touch();

        if (this.$v.forgot_password.$anyError) {
            return;
        }

        this.$bvToast.toast('Link forgot password berhasil kami kirimkan ke email anda', {
            title: 'Success',
            variant: 'success',
            solid: true
        })
        
        setTimeout(() => this.$router.push({ path: '/'}), 3000);
    }
  }
}
</script>
