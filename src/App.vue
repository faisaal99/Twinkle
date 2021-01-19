<template>
<div id="app">
  <nav>
    <router-link to="/">
      <div class="navigation__logo">Twinkle</div>
    </router-link>
    
    <div class="navigation__user" v-if="user">{{ user.userName }}</div>
  </nav>

  <router-view />
</div>
</template>

<script>
import { computed } from 'vue';
import { useStore } from 'vuex';

export default {
  name: 'App',
  setup() {
    const store = useStore();
    const user = computed(() => store.state.User.user);

    return {
      user
    };
  }
}
</script>

<style lang="scss">
#app {
  font-family: 'PT Sans', Arial, sans-serif;
  color: #2c3e50;
  min-height: 100vh;
  background-color: #f3f5fa;

  nav {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 10px 5%;
    background-color: deeppink;
    color: white;

    .navigation__logo {
      font-weight: bold;
      font-size: 2rem;
    }

    .navigation__user {
      font-weight: bold;
    }
  }
}

@import url('https://fonts.googleapis.com/css2?family=PT+Sans&display=swap');
</style>
