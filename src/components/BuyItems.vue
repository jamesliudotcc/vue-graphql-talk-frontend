<template>
  <div>
    <hr>Buy Items Component
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
    </form>
  </div>
</template>

<script>
import USER from '../graphql/User.gql';
import STORES from '../graphql/Stores.gql';

export default {
  name: 'BuyItems',
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
    // Only show items when its stores property includes
    // the id for the store chosen in the dropdown.
    items: function() {
      const allItems = this.user.houses[this.whichHouse].items;
      return allItems.filter(item => {
        if (item.stores.map(store => store.id).includes(this.whichStore))
          return true;
      });
    },
  },
};
</script>
