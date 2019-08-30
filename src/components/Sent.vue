<template>
  <h1>Sent</h1>
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
    sentMessages() {
      return this.messages.filter(message => {
        return message.type === "outgoing" && !message.isDeleted;
      });
    }
  }
};
</script>

<style>
</style>
