<template>
  <h1>Trash</h1>
</template>

<script>
export default {
  props: {
    data: {
      type: Object,
      required: true
    }
  },
  computed: {
    trashedMessages() {
      return this.messages.filter(message => {
        return message.isDeleted;
      });
    }
  }
};
</script>

<style>
</style>
