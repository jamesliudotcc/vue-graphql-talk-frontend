<template>
  <div>
    <hr>Purchase Items Component
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
      <select name="select-store" id="select-store" v-model="whichStore">
        <option v-for="store in stores" :key="`store-${store.id}`" :value="store.id">{{store.name}}</option>
      </select>
      <ul>
        <li v-for="item in items" :key="`item-${item}`">
          <input type="checkbox" :value="item.id" v-model="itemsPurchased">
          {{item.name}}
        </li>
      </ul>
      <button type="submit" v-on:click.prevent="purchaseItems">Bought</button>
    </form>
  </div>
</template>

<script>
import USER from '../graphql/User.gql';
import STORES from '../graphql/Stores.gql';
import PURCHASEITEMS from '../graphql/PurchaseItems.gql';

export default {
  name: 'PurchaseItems',
  apollo: {
    user: USER,
    stores: STORES,
  },
  data: function() {
    return {
      whichHouse: 0,
      whichStore: 0,
      itemsPurchased: [],
    };
  },
  computed: {
    items: function() {
      const allItems = this.user.houses[this.whichHouse].items;
      const unpurchasedItems = allItems.filter(item => !item.done);

      // Only show items when its stores property includes
      // the id for the store chosen in the dropdown.
      return unpurchasedItems.filter(item => {
        if (item.stores.map(store => store.id).includes(this.whichStore))
          return true;
      });
    },
  },

  methods: {
    purchaseItems() {
      this.$apollo
        .mutate({
          mutation: PURCHASEITEMS,
          variables: {
            house: this.whichHouse,
            itemIds: this.itemsPurchased,
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
