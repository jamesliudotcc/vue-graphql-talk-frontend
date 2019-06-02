<template>
  <div>
    <!--  -->
    <hr>Add Item Component
    <form>
      <h6>House</h6>
      <select name="select-house" id="select-house" v-model="whichHouse">
        <option
          v-for="house in user.houses"
          :value="house.id"
          :key="`house-${house.id}`"
        >{{house.name}}</option>
      </select>
      <h6>Store</h6>
      <ul>
        <li v-for="store in stores" :key="`store-${store.id}`">
          <input
            type="checkbox"
            :name="`store-${store.id}`"
            :id="`store-${store.id}`"
            :value="store.id"
            v-model="whichStores"
          >
          <label :for="`store-${store.id}`">{{store.name}}</label>
        </li>
      </ul>
      <input type="text" placeholder="Item" v-model="newItem">
      <button type="submit" v-on:click.prevent="addItem">Add Item</button>
    </form>
  </div>
</template>

<script>
import USER from '../graphql/User.gql';
import STORES from '../graphql/Stores.gql';
import CREATEITEM from '../graphql/CreateItem.gql';

export default {
  name: 'AddItem',
  apollo: {
    user: USER,
    stores: STORES,
  },
  data: function() {
    return {
      newItem: '',
      whichStores: [],
      whichHouse: 0,
    };
  },
  methods: {
    async addItem() {
      if (!this.newItem) return;
      if (!this.whichStores.length) return;

      this.$apollo
        .mutate({
          mutation: CREATEITEM,
          variables: {
            name: this.newItem,
            house: this.whichHouse,
            stores: this.whichStores,
            qty: 1,
          },
        })
        .then(() => {
          this.$apollo.queries.user.refetch();
          this.newItem = '';
        });
    },
  },
};
</script>
