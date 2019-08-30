<template>
  <div class="inbox-body">
    <h1>Important</h1>
    <app-messages :messages="importantMessages"></app-messages>
  </div>
</template>

<script>
import Messages from "./Messages";

export default {
  components: {
    appMessages: Messages
  },
  props: {
    data: {
      type: Object,
      required: true
    }
  },
  computed: {
    importantMessages() {
      return this.data.messages.filter(message => {
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
