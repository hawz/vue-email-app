<template>
  <div class="inbox-body">
    <h1>Trash</h1>
    <app-messages :messages="trashedMessages"></app-messages>
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
    trashedMessages() {
      return this.data.messages.filter(message => {
        return message.isDeleted;
      });
    }
  }
};
</script>

<style>
</style>
