<template>
  <div class="users-list">
    <router-link v-for="user in users" :key="user.id" :to="{name:'UserProfile', params: {userId:user.id}}">
      @{{ user.username }}
      <small>{{ user.email }}</small>
    </router-link>
  </div>


</template>

<script>

import {users} from "@/assets/users";

export default {
  name: 'Home',
  setup() {
    return {users};
  }
}
</script>


<style lang="scss">

.users-list {

  display: flex;
  justify-content: flex-start;
  align-items: flex-start;

  a {
    margin-right: 0.2rem;

    &:link, &:visited {
      padding: 0.5rem 2rem;
      background: white;
      color: darkslateblue;
      font-size: 1.1rem;
    }

    small {
      display: block;
      font-size: 0.9rem;
      color: darkgrey;
    }

  }
}


</style>
