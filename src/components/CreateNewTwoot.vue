<template>
  <form @submit.prevent="createNewTwoot" class="create-toot-form" :class="{'__exceeded':twootCharCount > 100}">
    <label>Twoot Message <small>({{ twootCharCount }}/100)</small></label>
    <textarea rows="5" cols="20" v-model="state.twootMsg"></textarea>

    <label>Twoot Type</label>
    <select v-model="state.twootType">
      <option :value="option.value" v-for="(option,index) in state.twootTypes" :key="index">{{ option.label }}</option>
    </select>

    <button>Twoot!</button>

  </form>
</template>

<script>

import {reactive, computed} from 'vue';

export default {
  name: "CreateNewTwoot",
  setup(props, ctx) {
    const state = reactive({
      twootMsg: '',
      twootType: 'instant',
      twootTypes: [
        {value: 'draft', label: 'Draft'},
        {value: 'instant', label: 'Instant Twoot'}
      ]
    });

    const twootCharCount = computed(() => state.twootMsg.length);

    function createNewTwoot() {
      if (state.twootMsg && state.twootType === "instant") {

        ctx.emit('add-twoot', state.twootMsg);
        state.twootMsg = '';
      }
    }

    return {state, twootCharCount, createNewTwoot};
  },
}
</script>

<style lang="scss" scoped>

.create-toot-form {

  label {
    font-size: 0.8rem;
    display: block;

    small {
      color: darkgrey;
    }

  }

  textarea {
    border: solid 1px lightgrey;
    padding: 0.5rem;
    font-family: Avenir, Helvetica, Arial, sans-serif;
  }

  select {
    border: solid 1px lightgrey;
  }

  button {
    display: inline-block;
    width: 80%;
    margin: 0 auto;
    text-align: center;
    padding: 0.8rem 1.5rem;
    background: dodgerblue;
    color: white;
    border: none;
    font-size: 1rem;
    text-transform: uppercase;
    margin-top: 1rem;
    cursor: pointer;

    &:hover {
      background: darkcyan;
    }

    &:active, &:focus {
      border: none;
      outline: none;
    }
  }

  small {
    font-size: 0.85rem;
  }

  &.__exceeded {
    color: red !important;

    textarea {
      border-color: red;

      &:focus, &:active {
        border-color: red;
        outline-color: red;
      }

    }
  }
}


</style>