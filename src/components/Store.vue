<template>
  <div>
    <ul>
      <li v-for="store in stores" v-bind:key="`store-${store.id}`">{{store.name}}</li>
    </ul>
    <form>
      <input type="text" placeholder="Add Store" v-model="newStore">
      <button v-on:click.prevent="addStore" type="submit">Submit</button>
    </form>
  </div>
</template>

<script>
import CREATESTORE from '../graphql/CreateStore.gql';
import USER from '../graphql/User.gql';
import STORES from '../graphql/Stores.gql';

export default {
  name: 'Store',
  apollo: {
    stores: STORES,
  },

  data: function() {
    return { newStore: '' };
  },
  methods: {
    addStore() {
      if (!this.newStore) return;
      this.$apollo
        .mutate({
          mutation: CREATESTORE,
          variables: {
            name: this.newStore,
          },
        })
        .then(() => {
          this.$apollo.queries.stores.refetch();
          this.newStore = '';
        });
    },
  },
};
</script>
