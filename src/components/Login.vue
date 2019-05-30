<template>
  <div class="login">
    <form action="POST">
      <input v-model="email" type="email" name="email" id="email" placeholder="Email">
      <input
        v-model="password"
        type="password"
        name="password"
        id="password"
        placeholder="Password"
      >
      <button v-on:click.prevent="login" type="submit">Login</button>
    </form>
  </div>
</template>

<script>
import LOGIN from '../graphql/Login.gql';
// import gql from 'graphql-tag';

export default {
  name: 'Login',
  data() {
    return {
      email: '',
      password: '',
    };
  },
  methods: {
    async login() {
      const result = await this.$apollo.mutate({
        mutation: LOGIN,
        variables: {
          email: this.email,
          password: this.password,
        },
      });
      console.log(result);
      localStorage['apollo-token'] = result.data.login.token;
      this.$emit('input', true);
      // TODO: Add error handling for bad credentials
    },
  },
};
</script>
