<template>
  <div class="register">
    <form action="POST">
      <input v-model="name" type="text" name="name" id="register-name" placeholder="Name">
      <input v-model="email" type="email" name="email" id="register-email" placeholder="Email">
      <input
        v-model="password"
        type="password"
        name="password"
        id="register-password"
        placeholder="Password"
      >
      <button v-on:click.prevent="register" type="submit">Register</button>
    </form>
  </div>
</template>

<script>
import REGISTER from '../graphql/Register.gql';
// import gql from 'graphql-tag';

export default {
  name: 'Register',
  data() {
    return {
      name: '',
      email: '',
      password: '',
    };
  },
  methods: {
    async register() {
      const result = await this.$apollo.mutate({
        mutation: REGISTER,
        variables: {
          email: this.email,
          name: this.name,
          password: this.password,
        },
      });
      localStorage['apollo-token'] = result.data.register.token;
      this.$emit('input', true); // this pattern feels slightly hacky?
      // TODO: Add error handling for bad credentials
    },
  },
};
</script>
