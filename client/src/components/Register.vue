<template>
  <div>
    <h1>Register</h1>
    <br>
    <input
      type="email"
      name="email"
      v-model="emailAddress"
      placeholder="email"
      />
    <br>
    <input
      type="password"
      name="password"
      v-model="password"      
      placeholder="password"
      />
      <br>
      <button @click="registTheUser">Register</button>
      <br>
      <p>{{responseFromRegistering.message}}</p>
  </div>
</template>

<script>
import AuthenticationService from '@/services/AuthenticationService'
export default {
  name: 'Register',
  data () {
    return {
      emailAddress: '',
      password: '',
      responseFromRegistering:{
        message:''
      }
    }
  },
  methods:{
    /**
     * Better then promises these days?
     * A function has to be async to have await inside of it
     */
    async registTheUser(){
      const resp = await AuthenticationService.register({
        email    : this.emailAddress,
        password : this.password
      });
      this.emailAddress = '';
      this.password = '';
      this.responseFromRegistering = resp.data;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
