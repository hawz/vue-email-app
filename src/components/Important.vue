<template>
  <h1>Important</h1>
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
    importantMessages() {
      return this.messages.filter(message => {
        return (
          message.type === "incoming" &&
          message.isImportant &&
          !message.isDeleted
        );
      });
    }
  }
};
</script>

<style>
</style>
