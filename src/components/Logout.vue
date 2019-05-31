<template>
  <div class="logout">
    <form action="POST">
      <button v-on:click.prevent="logout" type="submit">Logout</button>
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
    async logout() {
      localStorage.removeItem('apollo-token');
      this.$emit('input', false); // this pattern feels slightly hacky?
    },
  },
};
</script>
