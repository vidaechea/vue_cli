<template>
  <div class="hello">
    <login :errorMessage="errorMessage" v-on:loginCredentials="checkCredentials"></login>
  </div>
</template>

<script>
import Login from './Login'
export default {
  name: 'HelloWorld',
  components: {
    Login: Login
  },
  data () {
    return {
      errorMessage: ''
    }
  },
  methods: {
    checkCredentials: function (event) {
      console.log('Email is ' + event.email)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
