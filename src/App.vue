<template>
  <div id="app">
    <register/>
    <login/>
    <logout/>
    <div v-if="localStorage['apollo-token']">
      <secret/>
    </div>
  </div>
</template>

<script>
// import ApolloExample from './components/ApolloExample.vue';
import Register from './components/Register.vue';
import Login from './components/Login.vue';
import Logout from './components/Logout.vue';
import Secret from './components/Secret.vue';

export default {
  name: 'app',
  components: {
    // ApolloExample,
    Login,
    Logout,
    Register,
    Secret,
  },
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
