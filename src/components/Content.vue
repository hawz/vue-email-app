<template>
  <aside class="lg-side">
    <div class="inbox-head">
      <h3>{{ currentView.title }}</h3>
    </div>

    <keep-alive>
      <component :is="currentView.tag"></component>
    </keep-alive>
  </aside>
</template>

<script>
import { eventBus } from "../main";
import Inbox from "./Inbox";
import Sent from "./Sent";
import Important from "./Important";
import Trash from "./Trash";
import ViewMessage from "./ViewMessage";

export default {
  components: {
    appInbox: Inbox,
    appSent: Sent,
    appImportant: Important,
    appTrash: Trash,
    appViewMessage: ViewMessage
  },
  data() {
    return {
      history: [
        {
          tag: "app-inbox",
          title: "Inbox"
        }
      ]
    };
  },
  computed: {
    currentView() {
      return this.history[0];
    }
  },
  created() {
    eventBus.$on("navigateTo", data => {
      const { tag, title } = data;
      // console.log("navigate to", data);
      this.history.unshift({
        tag,
        title
      });
    });
  }
};
</script>

<style>
</style>
