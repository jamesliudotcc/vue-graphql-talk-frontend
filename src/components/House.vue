<template>
  <div>
    <ul>
      <li v-for="house in houses" v-bind:key="`house-${house}`">{{house.name}}</li>
    </ul>
    <form>
      <input type="text" placeholder="Add House" v-model="newHouse">
      <button v-on:click.prevent="addHouse">Submit</button>
    </form>
  </div>
</template>

<script>
import gql from 'graphql-tag';

import CREATEHOUSE from '../graphql/CreateHouse.gql';
export default {
  name: 'House',
  apollo: {
    user: gql`
      # match apollo object property to name on query.
      query {
        user {
          name
          houses {
            id
            name
            users
            items {
              id
              name
              stores {
                id
                name
              }
            }
          }
        }
      }
    `,
  },
  computed: {
    houses: function() {
      return this.user.houses;
    },
  },
  data: function() {
    return { newHouse: '' };
  },
  methods: {
    async addHouse() {
      console.log(`add house ${this.newHouse}`);
      // TODO: Add call to GQL.
    },
  },
};
</script>
