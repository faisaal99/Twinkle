<template>
  <div class="twinkle-item" @click="favoriteTwinkle(twinkle.id)">
    <div class="user-profile__twinkle">
      <div class="twinkle-item__user" style="margin-bottom: 10px">
        {{ fullName }}
      </div>
      <div class="twinkle-item__content">
        {{ twinkle.content }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "TwinkleItem",
  props: {
    fullName: {
      type: String,
      required: true
    },
    twinkle: {
      type: Object,
      required: true
    }
  },
  methods: {
    favoriteTwinkle(id) {
      this.$emit("favorite", id);
    }
  }
}
</script>

<style lang="scss" scoped>
.twinkle-item {
  padding: 20px;
  background-color: white;
  border-radius: 5px;
  border: 1px solid #dfe3e8;
  box-sizing: border-box;
  cursor: pointer;
  transition: all 0.25s ease;
  margin-bottom: 10px;

  .twinkle-item__user {
    font-weight: bold;
  }

  &:hover {
    border: 1px solid darkgray;
  }
}
</style>