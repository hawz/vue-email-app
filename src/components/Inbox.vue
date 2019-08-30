<template>
  <div class="inbox-body">
    <div class="mail-option">
      <div class="btn-group">
        <a href="#" class="btn" @click="refresh">
          <i class="fa fa-refresh"></i>&nbsp; refresh
        </a>
      </div>
    </div>
    <app-messages :messages="incomingMessages"></app-messages>
  </div>
</template>

<script>
import Messages from "./Messages";
import { eventBus } from "../main";

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
  methods: {
    refresh() {
      eventBus.$emit("refreshMessages");
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
