<template>
  <div class="inbox-body">
    <h1>Inbox</h1>
    <app-messages :messages="incomingMessages"></app-messages>
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
    incomingMessages() {
      return this.data.messages.filter(message => {
        return message.type === "incoming" && !message.isDeleted;
      });
    }
  }
};
</script>

<style>
</style>
