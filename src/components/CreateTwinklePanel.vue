<template>
  <form class="create-twinkle-panel" @submit.prevent="createNewTwinkle" :class="{'--exceeded': newTwinkleCharacterCount > 180}">
    <label for="newTwinkle"><strong>New Twinkle</strong> ({{ newTwinkleCharacterCount }}/180)</label>
    <textarea id="newTwinkle" rows="4" placeholder="Write a new Twinkle... " v-model="state.newTwinkleContent"/>

    <div class="create-twinkle-panel__submit">
      <div class="create-twinkle-type">
        <label for="newTwinkleType"><strong>Type: </strong></label>
        <select id="newTwinkleType" v-model="state.selectedTwinkleType">
          <option :value="option.value" v-for="(option, index) in state.twinkleTypes" :key="index">
            {{ option.name }}
          </option>
        </select>
      </div>

      <input class="create-twinkle-submit-btn" type="submit" value="Post" /> 
    </div>

  </form>
</template>

<script>
import { reactive, computed } from 'vue';

export default {
  name: "CreateTwinklePanel",
  setup(props, ctx) {
    const state = reactive({
      newTwinkleContent: '',
      selectedTwinkleType: 'instant',
      twinkleTypes: [
        { value: 'draft', name: 'Draft' },
        { value: 'instant', name: 'Instant Twinkle' }
      ]
    })

    const newTwinkleCharacterCount = computed(() => state.newTwinkleContent.length)

    function createNewTwinkle() {
      if (state.newTwinkleContent && state.selectedTwinkleType !== 'draft' && state.newTwinkleContent.length <= 180) {
        ctx.emit('add-twinkle', state.newTwinkleContent);
        state.newTwinkleContent = '';
      }
    }

    return {
      state,
      newTwinkleCharacterCount,
      createNewTwinkle
    }
  }
}
</script>

<style lang="scss" scoped>
.create-twinkle-panel {
  margin-top: 20px;
  padding: 20px 0;
  display: grid;
  gap: 10px;

  textarea {
    border: 1px solid #dfe3e8;
    border-radius: 5px;
    padding: 5px;
    transition: 0.2s ease;
    font-family: 'PT Sans', Arial, sans-serif;

    &:hover {
      border: 1px solid darkgray;
    }

    &:focus {
      outline: none;
      border: 1px solid black;
    }

    &::placeholder {
      font-family: 'PT Sans', Arial, sans-serif;
    }
  }

  .create-twinkle-panel__submit {
    display: flex;
    flex-direction: column;
    justify-content: space-between;

    .create-twinkle-type {
      padding: 10px 0;
    }

    .create-twinkle-submit-btn {
      padding: 5px 20px;
      margin: auto 0;
      border-radius: 5px;
      border: none;
      background-color: deeppink;
      color: white;
      font-weight: bold;
      transition: 0.2s ease;

      &:hover {
        cursor: pointer;
        background-color: rgb(255, 93, 179);
      }
    }
  }

  &.--exceeded {
    color: crimson;
    border-color: crimson;

    .create-twinkle-submit-btn {
      background-color: #d3d4d6;
      color: rgb(110, 110, 110);

      &:hover {
        background-color: #d3d4d6;
        cursor: not-allowed;
      }

      &:focus {
        outline:none;
      }
    }

    textarea {
      &:focus {
        border: 1px solid crimson;
      }
    }
  }

  #newTwinkle {
    resize: none;
  }
}
</style>