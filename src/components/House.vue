<template>
  <div>
    <ul>
      <li v-for="house in user.houses" v-bind:key="`house-${house}`">{{house.name}}</li>
    </ul>
    <form>
      <input type="text" placeholder="Add House" v-model="newHouse">
      <button v-on:click.prevent="addHouse" type="submit">Submit</button>
    </form>
  </div>
</template>

<script>
import gql from 'graphql-tag';

import CREATEHOUSE from '../graphql/CreateHouse.gql';
import USER from '../graphql/User.gql';
export default {
  name: 'House',
  apollo: {
    user: USER,
  },

  data: function() {
    return { newHouse: '' };
  },
  methods: {
    async addHouse() {
      // TODO: Add call to GQL.
      const result = await this.$apollo.mutate({
        mutation: CREATEHOUSE,
        variables: {
          name: this.newHouse,
        },
      });
    },
  },
};
</script>
