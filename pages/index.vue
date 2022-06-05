<template>
    <b-container>
        <b-form @submit.stop.prevent="onSubmit">
            <b-form-group id="username-input">
                <b-form-input
                type="text"
                placeholder="Username" 
                class="form-control"
                v-model="$v.login.username.$model"
                :state="validateState('username')"
                aria-describedby="username-input-feedback"
                ></b-form-input>

                <b-form-invalid-feedback
                id="username-input-feedback"
                >Username is a required.</b-form-invalid-feedback>
            </b-form-group>

            <b-form-group id="password-input">
                <b-form-input
                type="password"
                placeholder="Password" 
                class="form-control"
                v-model="$v.login.password.$model"
                :state="validateState('password')"
                aria-describedby="password-input-feedback"
                ></b-form-input>

                <b-form-invalid-feedback
                id="password-input-feedback"
                >Password is a required.</b-form-invalid-feedback>
            </b-form-group>

            <b-row>
                <b-col cols="7">
                    <b-form-checkbox value="me" class="small">Keep me signed in</b-form-checkbox>
                </b-col>
                <b-col cols="5" class="text-right">
                    <NuxtLink to="/forgot-password" class="small">Forgot Password</NuxtLink>
                </b-col>
            </b-row>
            <div class="mb-5 mt-5 text-center">
                <b-button 
                    variant="primary"
                    size="lg"
                    type="submit" 
                >
                    LOG IN
                </b-button>
            </div>
        </b-form>
    </b-container>
</template>

<script>
import { validationMixin } from "vuelidate";
import { required } from 'vuelidate/lib/validators'
export default {
  layout: 'user-access',
  mixins: [validationMixin],
  data(){
      return{
        login :{
            username: '',
            password: '',
        }
      }
  },
  validations: {
      login: {
            username: {
                required
            },
            password: {
                required
            }
      }
  },
  methods: {
    validateState(username) {
        const { $dirty, $error } = this.$v.login[username];
        return $dirty ? !$error : null;
    },
    validateState(password) {
        const { $dirty, $error } = this.$v.login[password];
        return $dirty ? !$error : null;
    },
    onSubmit() {
        this.$v.login.$touch();

        if (this.$v.login.$anyError) {
            return;
        }

        this.$bvToast.toast('Login Berhasil', {
            title: 'Success',
            variant: 'success',
            solid: true
        })

        setTimeout(() => this.$router.push({ path: '/dashboard'}), 3000);
    }
  }
}
</script>
