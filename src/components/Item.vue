<template>
  <div>
    <!--  -->
    <hr>Item Component
    <form>
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
      <input type="text" placeholder="Item" v-model="newItem">
    </form>
  </div>
</template>

<script>
import USER from '../graphql/User.gql';
import STORES from '../graphql/Stores.gql';
export default {
  name: 'Item',
  apollo: {
    user: USER,
    stores: STORES,
  },
  data: function() {
    return {
      newItem: '',
      whichStores: [],
    };
  },
};
</script>
