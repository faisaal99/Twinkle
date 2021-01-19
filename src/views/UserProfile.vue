<template>
  <div class="user-profile">
    <div class="user-profile__sidebar">
      <div class="user-profile__user-panel">
        <h2 class="user-profile__full-name">{{ fullName }}</h2>
        <p class="user-profile__username">@{{ state.user.userName }}</p>

        <div class="user-profile__admin-badge" v-if="state.user.isAdmin">
          Admin
        </div>

        <div class="user-profile__follower-count">
          <strong>Followers:</strong> {{ state.followers }}
        </div>
      </div>
      <CreateTwinklePanel @add-twinkle="addTwinkle" />
    </div>
    

    <div class="user-profile__twinkles-wrapper">
        <TwinkleItem 
          v-for="twinkle in state.user.twinkles" 
          :key="twinkle.id" 
          :fullName="fullName" 
          :twinkle="twinkle"
        />

        <h3 v-if="state.user.twinkles.length === 0">No posts ... yet</h3>
    </div>
    
  </div>
</template>

<script>
import { reactive, computed } from 'vue';
import { useRoute } from 'vue-router';

import { users } from "../assets/users";

import CreateTwinklePanel from "../components/CreateTwinklePanel";
import TwinkleItem from "../components/TwinkleItem";

export default {
  name: "UserProfile",
  components: { TwinkleItem, CreateTwinklePanel },
  setup() {
    const route = useRoute();
    const userId = computed(() => route.params.userId);

    const state = reactive({
      followers: 0,
      user: users[userId.value - 1] || users[0]
    });

    const fullName = computed(() => `${state.user.firstName} ${state.user.lastName}`);

    function addTwinkle(twinkle) {
      state.user.twinkles.unshift({ id: state.user.twinkles.length + 1, content: twinkle });
    }

    return {
      state,
      fullName,
      addTwinkle,
      userId
    }
  }
}
</script>

<style lang="scss" scoped>
.user-profile {
  display: grid;
  grid-template-columns: 1fr 3fr;
  gap: 50px;
  padding: 50px 5%;

  .user-profile__user-panel {
    display: flex;
    flex-direction: column;
    padding: 20px;
    background-color: white;
    border-radius: 5px;
    border: 1px solid #dfe3e8;
    transition: 0.2s;

    &:hover {
      border: 1px solid darkgray;
    }

    h1, h2 {
      margin: 0;
    }

    .user-profile__admin-badge {
      background-color: #a62bcc;
      color: white;
      border-radius: 5px;
      margin: 10px 0;
      margin-right: auto;
      padding: 4px 10px;
      font-weight: bold;
    }
  }

  .user-profile__twinkles-wrapper {
    display: grid;
    gap: 10px;
    margin-bottom: auto;
  }
}
</style>