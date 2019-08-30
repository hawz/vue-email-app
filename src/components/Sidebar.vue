<template>
  <aside class="sm-side">
    <app-user></app-user>

    <ul class="inbox-nav">
      <li :class="{active: activeView === 'app-inbox'}">
        <a href="#" @click.prevent="navigate('app-inbox', 'Inbox')">
          <i class="fa fa-inbox"></i>Inbox
          <span class="label label-danger pull-right">?</span>
        </a>
      </li>

      <li :class="{active: activeView === 'app-sent'}">
        <a href="#" @click.prevent="navigate('app-sent', 'Sent')">
          <i class="fa fa-envelope-o"></i>Sent
          <span class="label label-default pull-right">?</span>
        </a>
      </li>

      <li :class="{active: activeView === 'app-important'}">
        <a href="#" @click.prevent="navigate('app-important', 'Important')">
          <i class="fa fa-bookmark-o"></i>Important
          <span class="label label-warning pull-right">?</span>
        </a>
      </li>

      <li :class="{active: activeView === 'app-trash'}">
        <a href="#" @click.prevent="navigate('app-trash', 'Trash')">
          <i class="fa fa-trash-o"></i>Trash
          <span class="label label-default pull-right">?</span>
        </a>
      </li>
    </ul>
  </aside>
</template>

<script>
import { eventBus } from "../main";
import User from './User';

export default {
  components: {
    appUser: User
  },
  data() {
    return {
      activeView: "app-inbox"
    };
  },
  methods: {
    navigate(tag, title) {
      this.activeView = tag;
      eventBus.$emit("navigateTo", {
        tag,
        title
      });
    }
  }
};
</script>

<style>
</style>
