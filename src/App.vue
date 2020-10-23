<template>

  <nav>
    <div class="container">
      <div class="logo">
        <router-link to="/">VueJS</router-link>
      </div>
      <div class="username" v-if="user">@{{ user.username }}</div>
    </div>
  </nav>

  <div id="main-content">
    <div class="container">
      <router-view/>
    </div>
  </div>


</template>

<script>

import {useStore} from 'vuex';
import {computed} from 'vue';

export default {
  name: 'App',
  setup() {

    const store = useStore();
    const user = computed(() => store.state.User.user);

    return {user};

  }


}
</script>

<style lang="scss">

#app {
  display: flex;
  justify-content: flex-start;
  flex-wrap: wrap;
  flex-direction: column;

  margin: 0 auto;
}

.container {
  width: 1200px;
  margin: 0 auto;
}


nav {
  background: darkslateblue;
  height: 4rem;
  padding: 0 2rem;
  margin-bottom: 4rem;

  .logo {
    font-weight: 600;
    font-size: 1.4rem;

    a {
      text-decoration: none;

      &:link, &:visited {
        color: white;
      }

      &:hover {
        color: aqua;
      }
    }
  }

  .container {
    display: flex;
    justify-content: space-between;
    align-items: center;
    color: white;
    height: 100%;
  }


}


</style>
