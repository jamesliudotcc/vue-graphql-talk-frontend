<template>
  <div>
    <hr>

    <!-- TODO: Create component that decides whether to show no houses to join
    or the join a house component. v-if and v-for do not mix.-->

    <form>
      <h6>Join a House</h6>
      <div v-if="!showHouseSelector">No houses to join</div>
      <select name="select-house-join" id="select-house-join" v-model="houseToJoin">
        <option
          v-for="house in openHouses"
          v-bind:key="`join-house-${house.id}`"
          :value="house.id"
        >{{house.name}}</option>
      </select>
      <button type="submit" v-on:click.prevent="joinHouse">Join House</button>
    </form>
  </div>
</template>

<script>
import HOUSES from '../graphql/Houses.gql';
import JOINHOUSE from '../graphql/JoinHouse.gql';
import USER from '../graphql/User.gql';

export default {
  name: 'JoinHouse',
  apollo: {
    houses: HOUSES,
    user: USER,
  },

  data: function() {
    return {
      houseToJoin: 0,
    };
  },
  computed: {
    openHouses: function() {
      const alreadyMemberOf = this.user.houses.map(house => house.id);
      const allHouseIds = this.houses.map(house => house.id);

      return allHouseIds
        .filter(house => {
          if (!alreadyMemberOf.includes(house)) return true;
        })
        .map(houseId => this.houses[houseId]);
    },
    showHouseSelector: function() {
      if (this.openHouses.length) return true;
      else return false;
    },
  },

  methods: {
    joinHouse() {
      this.$apollo
        .mutate({
          mutation: JOINHOUSE,
          variables: { house: this.houseToJoin },
        })
        .then(() => {
          this.$apollo.queries.user.refetch();
          this.newItem = '';
        });
    },
  },
};
</script>
