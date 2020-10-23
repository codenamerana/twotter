<template>
  <div class="twoot-item" @click="favouriteTwoot(twoot.id)">
    <p>{{ twoot.content }}</p>
  </div>

</template>

<script>
export default {
  name: "UserTwoot",
  props: {
    twoot: {
      type: Object,
      required: true
    }
  },
  methods: {
    favouriteTwoot(id) {
      this.$emit('favourite', id);
    }
  }
}
</script>

<style scoped lang="scss">

.twoot-item {
  background: white;
  padding: 0.5rem 1rem;
  width: 900px;
  margin-bottom: 0.5rem;
  transition: 0.3s;

  &:hover {
    cursor: pointer;
    transform: scale(1.04);
    transition: 0.3s;
  }

  p {
    font-size: 0.75rem;
  }
}

</style>