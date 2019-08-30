<template>
  <div>
    <a
      href="#composeModal"
      data-toggle="modal"
      class="btn btn-compose"
      @click.prevent="showModal = true"
    >Compose</a>

    <div>
      <div
        class="modal-dialog"
        :class="{'show-modal': showModal, 'hidden': !showModal}"
        role="document"
      >
        <div class="modal-content">
          <div class="modal-header">
            <button
              aria-hidden="true"
              data-dismiss="modal"
              class="close"
              aria-label="Close"
              type="button"
              @click.prevent="showModal = false"
            >&times;</button>
            <h4 aria-label="composeModalLabel" class="modal-title">New Message</h4>
          </div>

          <div class="modal-body">
            <form @submit.prevent="sendMessage" role="form" class="form-horizontal">
              <div class="form-group">
                <label class="col-lg-2 control-label" for="subject">Subject</label>
                <div class="col-lg-10">
                  <input type="text" v-model="message.subject" id="subject" class="form-control" />
                </div>
              </div>

              <div class="form-group">
                <label class="col-lg-2 control-label" for="message">Message</label>
                <div class="col-lg-10">
                  <textarea
                    v-model="message.content"
                    rows="10"
                    cols="30"
                    class="form-control"
                    id="message"
                  ></textarea>
                </div>
              </div>

              <div class="form-group">
                <div class="col-lg-offset-2 col-lg-10">
                  <button class="btn btn-send" type="submit">Send</button>
                </div>
              </div>
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { eventBus } from "../main";
import moment from "moment";

export default {
  data() {
    return {
      message: {
        subject: "",
        content: ""
      },
      showModal: false
    };
  },
  methods: {
    sendMessage() {
      eventBus.$emit("sentMessage", {
        message: {
          subject: this.message.subject,
          content: this.message.content,
          isDeleted: false,
          type: "outgoing",
          date: moment(),
          from: {
            name: "Albe Masia",
            email: "hawz@github.io"
          },
          attachments: []
        }
      });
      this.message.subject = "";
      this.message.content = "";
      this.showModal = false;
    }
  }
};
</script>

<style>
</style>
