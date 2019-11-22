<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Home</router-link>|
      <router-link to="/todomvc">Todomvc</router-link>|
      <router-link to="/users">Users</router-link>|
      <router-link to="/followers">{{$store.state.nb_followers.length || 0 }} followers</router-link>
    </div>
    <div v-if="$store.state.user">
      <h1>{{$store.state.user.name}}</h1>
      <button @click="$store.dispatch('logout')">logout</button>
    </div>
    <div v-else>
      <button @click="$store.dispatch('login')">login</button>
    </div>
    <router-view/>
  </div>
</template>

