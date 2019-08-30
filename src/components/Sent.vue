<template>
  <div class="inbox-body">
    <h1>Sent</h1>
    <app-messages :messages="sentMessages"></app-messages>
  </div>
</template>

<script>
import Messages from './Messages'

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
    sentMessages() {
      return this.data.messages.filter(message => {
        return message.type === "outgoing" && !message.isDeleted;
      });
    }
  }
};
</script>

<style>
</style>
