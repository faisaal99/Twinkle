<template>
  <div class="home">
    <h1>Welcome to Twinkle</h1>

    <div class="users-list">
      <router-link v-for="(user) in users" :to="{ name: 'UserProfile', params: { userId: user.id }}" :key="user.id">
        {{ user.userName }}
      </router-link>
    </div>
  </div>
</template>

<script>
import { users } from "../assets/users";

export default {
  name: 'Home',
  setup() {
    return {
      users
    }
  }
}
</script>

<style lang="scss" scoped>
.home {
  padding: 50px 5%;
}

.users-list {
  display: grid;
  gap: 10px;
}
</style>
