<template>
  <div class="container-fluid">
    <div class="row">
      <div class="col-xs-12 col-sm-6 col-s,-offset-3">
        <div class="card border-primary">
          <div class="card-header bg-primary text-white">
            Login
          </div>
          <div class="card-body">
            <form @submit.prevent="submitLogin">
              <div class="form-group">
                <label for="email">Email</label>
                <input ref="txtEmail" type="email" v-bind:class="[emailClass]" @input="checkEmailValidation" id="email" aria-describedby="emailHelp" placeholder="Enter email" autofocus required>
                <small id="emailHelp" class="form-text text-muted">We'll never share your email with anyone else.</small>
              </div>
              <div class="form-group">
                <label for="password">Password</label>
                <input ref="txtPassword" type="password" v-bind:class="[passwordClass]" @input="checkPasswordValidation" id="password" placeholder="Password" required>
              </div>
              <div v-if="errorMessage" class="text-center text-danger">{{ errorMessage }}</div>
              <button :disabled="submitBtnDisabled" class="btn btn-primary pull-right">Sign in</button>
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Login',
  props: {
    errorMessage: {
      type: String,
      required: false,
      default: ''
    }
  },
  data () {
    return {
      emailClass: '',
      passwordClass: '',
      submitBtnDisabled: true
    }
  },
  methods: {
    checkEmailValidation: function () {
      if (this.$refs.txtEmail.checkValidity()) {
        this.emailClass = 'form-control is-valid'
        if (this.$refs.txtPassword.checkValidity()) this.submitBtnDisabled = false
      } else {
        this.emailClass = 'form-control is-invalid'
        this.submitBtnDisabled = true
      }
    },
    checkPasswordValidation: function () {
      if (this.$refs.txtPassword.checkValidity()) {
        this.passwordClass = 'form-control is-valid'
        if (this.$refs.txtEmail.checkValidity()) this.submitBtnDisabled = false
      } else {
        this.passwordClass = 'form-control is-invalid'
        this.submitBtnDisabled = true
      }
    },
    submitLogin: function () {
      let email = this.$refs.txtEmail.value.trim()
      let password = this.$refs.txtPassword.value.trim()

      this.$emit('loginCredentials',
        {
          'email': email,
          'password': password
        }
      )
    }
  }
}
</script>

<style scoped>

</style>
