<template>
  <div id="app">
    <div v-if="!loggedIn">
      <register v-model="loggedIn"/>
      <login v-model="loggedIn"/>
    </div>
    <div v-if="loggedIn">
      <logout v-model="loggedIn"/>
      <secret/>
      <house/>
      <join-house/>
      <store/>
      <add-item/>
      <purchase-items/>
    </div>
  </div>
</template>

<script>
// import ApolloExample from './components/ApolloExample.vue';
import AddItem from './components/AddItem.vue';
import House from './components/House.vue';
import JoinHouse from './components/JoinHouse.vue';
import Login from './components/Login.vue';
import Logout from './components/Logout.vue';
import PurchaseItems from './components/PurchaseItems.vue';
import Register from './components/Register.vue';
import Secret from './components/Secret.vue';
import Store from './components/Store.vue';

export default {
  name: 'app',
  components: {
    // ApolloExample,
    AddItem,
    House,
    JoinHouse,
    Login,
    Logout,
    PurchaseItems,
    Register,
    Secret,
    Store,
  },
  data() {
    return {
      loggedIn: false,
    };
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
