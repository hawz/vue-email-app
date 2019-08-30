<template>
  <aside class="lg-side">
    <div class="inbox-head">
      <h3>{{ currentView.title }}</h3>
    </div>

    <keep-alive>
      <component :is="currentView.tag" :data="currentView.data"></component>
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
  props: {
    messages: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      history: [
        {
          tag: "app-inbox",
          title: "Inbox",
          data: {
            messages: null
          }
        }
      ]
    };
  },
  computed: {
    currentView() {
      let current = this.history[0];
      current.data.messages = this.messages;
      return current;
    }
  },
  created() {
    eventBus.$on("changeView", data => {
      const { tag, title } = data;
      this.history.unshift({
        tag,
        title,
        data: data.data || {}
      });
    });
  }
};
</script>

<style>
</style>
