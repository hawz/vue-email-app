<template>
  <div class="inbox-body">
    <div class="mail-option">
      <button class="btn btn-primary" @click="navigateBack">
        <i class="fa fa-arrow-left" aria-hidden="true"></i>&nbsp; Back
      </button>&nbsp;

      <button class="btn btn-danger" @click="data.message.isDeleted = true" :disabled="data.message.isDeleted">
        <i class="fa fa-trash-o" aria-hidden="true"></i>&nbsp; {{ data.message.isDeleted ? 'Deleted' : 'Delete' }}
      </button>&nbsp;

      <button class="btn" :class="{'btn-success': !data.message.isRead, 'btn-default': data.message.isRead}" @click="data.message.isRead = !data.message.isRead">
        <template v-if="data.message.isRead">
          <i class="fa fa-envelope" aria-hidden="true"></i>&nbsp; Mark as unread
        </template>
        <template v-else>
          <i class="fa fa-envelope-open" aria-hidden="true"></i>&nbsp; Mark as read
        </template>
      </button>&nbsp;

    </div>
    <p>
      <strong>Date:</strong>
      {{data.message.date.fromNow()}}
    </p>
    <p>
      <strong>From:</strong>
      {{data.message.from.name}} &lt;{{ data.message.from.email }}&gt;
    </p>
    <hr />
    <div v-html="data.message.content" class="message"></div>
    <div class="attachments" v-if="data.message.attachments.length > 0">
      <h4>Attachments</h4>
      <ul>
        <li v-for="(attachment, index) in data.message.attachments" :key="index">
          <i class="fa fa-paperclip"></i>
          {{attachment.fileName}} ({{attachment.size | formatBytes}})
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import { eventBus } from "../main";
export default {
  props: {
    data: {
      type: Object,
      isRequired: true
    }
  },
  methods: {
    navigateBack() {
      let previousView = this.$parent.previousView;

      eventBus.$emit("changeView", {
        tag: previousView.tag,
        title: previousView.title,
        data: previousView.data
      });
    }
  },
  activated() {
    if (typeof this.data.message.isRead !== "undefined") {
      this.data.message.isRead = true;
    }
  },
  filters: {
    formatBytes(bytes) {
      if (bytes === 0) {
        return "0 Bytes";
      }

      let decimals = 2;
      let k = 1000;
      let dm = decimals + 1 || 3;
      let sizes = ["Bytes", "KB", "MB", "GB", "TB", "PB", "EB", "ZB", "YB"];
      let i = Math.floor(Math.log(bytes) / Math.log(k));

      return parseFloat((bytes / Math.pow(k, i)).toFixed(dm)) + " " + sizes[i];
    }
  }
};
</script>

<style>
</style>
