<template>
  <div class="user-profile-container">
    <div class="user-profile-box">
    <span class="username">
          @{{ state.user.username }}
    </span>
      <span class="fullname">{{ fullName }} ({{ userId }})</span>
      <span class="admin" v-if="state.user.isAdmin">Administrator</span>
      <span class="followers">{{ state.followers }}</span>
      <small>Followers</small>
      <!--<button @click="followUser">Follow</button>-->

      <h4>Write a New Twoot</h4>
      <CreateNewTwoot @add-twoot="createNewTwoot"></CreateNewTwoot>

    </div>
    <div class="user-profile-twoot">
      <h3>Tweets from @{{ state.user.username }}</h3>
      <UserTwoot
          v-for="twoot in state.user.twoots"
          :key="twoot.id" :twoot="twoot"
          @favourite="toggleFavourite"></UserTwoot>
    </div>
  </div>


</template>

<script>

import UserTwoot from "@/components/UserTwoot";
import CreateNewTwoot from "@/components/CreateNewTwoot";
import {reactive, computed} from 'vue';
import {useRoute} from 'vue-router';
import {users} from "@/assets/users";

export default {
  name: "UserProfile",
  components: {CreateNewTwoot, UserTwoot},
  
  setup() {

    const route = useRoute();
    const userId = computed(() => route.params.userId);

    const state = reactive({
      followers: 0,
      user: users[userId.value - 1] || users[0]
    });

    
    const fullName = computed(() => `${state.user.firstName} ${state.user.lastName}`);


    function followUser() {
      state.followers++;
    }

    function toggleFavourite(id) {
      console.log(`Favourited Item: ${id}`);
    }

    function createNewTwoot(twootMsg) {
      state.user.twoots.unshift({
        id: state.user.twoots.length + 1, content: twootMsg
      });
    }

    return {state, fullName, followUser, toggleFavourite, createNewTwoot, userId}

  }

}
</script>

<style scoped lang="scss">


.user-profile-container {
  display: flex;
  justify-content: flex-start;

  .user-profile-box {
    background: white;
    width: 240px;

    display: flex;
    justify-content: center;
    align-content: center;
    flex-direction: column;
    text-align: center;
    margin-right: 0;
    margin-bottom: 0.5rem;
    padding: 2rem 0rem;
    position: relative;

    -webkit-box-shadow: 0px 0px 23px 0px rgba(0, 0, 0, 0.08);
    -moz-box-shadow: 0px 0px 23px 0px rgba(0, 0, 0, 0.08);
    box-shadow: 0px 0px 23px 0px rgba(0, 0, 0, 0.08);


    .username {
      font-size: 1.2rem;
      margin-bottom: 0.1rem;
      color: darkcyan;
      font-weight: 500;
    }

    .fullname {
      font-size: 0.85rem;
      padding: 0.3rem 1rem;
      text-align: center;
      opacity: 0.4;
    }

    .followers {
      font-size: 5rem;
      font-weight: lighter;
    }


    .admin {
      font-size: 0.5rem;
      padding: 0.2rem 0;
      width: 100%;
      text-align: center;
      text-transform: uppercase;
      background: ghostwhite;

      top: 1rem;
      left: 0;
      font-weight: 500;
      color: darkgoldenrod;
      letter-spacing: 2px;

    }


  }


}

.user-profile-twoot {
  margin-left: 2rem;
}


</style>