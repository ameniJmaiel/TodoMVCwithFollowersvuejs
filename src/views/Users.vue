<template>
  <div>
    <h1>USERS</h1>
    <ul>
      <li v-for="user in users" :key="user.id">
        <router-link :to="'/users/' + user.id">{{ user.name }}</router-link>|
        <button v-if="$store.getters.isFollower(user.id)" @click="unfollow(user)">unfollow</button>
        <button v-else @click="followUser(user)">Ajouter</button>

         |
      </li>
    </ul>
    <div v-if="$route.params.id">
      <router-view :key="$route.params.id"></router-view>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      users: []
    };
  },
  async mounted() {
    this.users = await fetch("https://jsonplaceholder.typicode.com/users").then(
      res => res.json()
    );
  },
  methods: {
    followUser(e) {
      this.$store.dispatch("follow", e);
    },
    unfollow(e) {
      this.$store.dispatch("unfollow", e);
    }
  }
};
</script>
