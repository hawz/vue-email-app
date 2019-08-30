<template>
  <div class="container">
    <div class="mail-box">
      <app-sidebar :messages="messages"></app-sidebar>
      <app-content :messages="messages"></app-content>
    </div>
  </div>
</template>

<script>
import Sidebar from "./components/Sidebar";
import Content from "./components/Content";
import messages from "./data/messages";
import randomMessages from "./data/random-messages";
import { eventBus } from "./main";

export default {
  components: {
    appSidebar: Sidebar,
    appContent: Content
  },
  data() {
    return {
      messages
    };
  },
  created() {
    eventBus.$on("refreshMessages", () => {
      let randomIndex = Math.floor(Math.random() * randomMessages.length);
      let temp = [randomMessages[randomIndex]];

      this.messages = [...temp, ...this.messages];
    });

    eventBus.$on("sentMessage", data => {
      let temp = [data.message];
      this.messages = [...temp, ...this.messages];
    });
  }
};
</script>

<style>
</style>
