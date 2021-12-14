<template>
  <v-container>
    <v-row>
      <v-col>
        <v-sheet min-height="20vh" rounded="lg">
          <!-- 채팅 화면 -->
          <Message v-bind:chat="chat" />
          <!-- 채팅 입력 -->
          <v-container>
            <v-row>
              <v-col>
                <div class="d-flex flex-row align-center">
                  <!-- 메세지 입력란 -->
                  <v-text-field
                    v-model="msg"
                    placeholder="Type Something"
                    @keypress.enter="send"
                  >
                  </v-text-field>
                  <!-- 팝업창 -->
                  <Popup v-on:uploadImage="addImage('user', $event)" />
                  <!-- 메세지 보내기 버튼 -->
                  <v-btn icon class="ml-4" @click="send">
                    <v-icon>mdi-send</v-icon>
                  </v-btn>
                </div>
              </v-col>
            </v-row>
          </v-container>
        </v-sheet>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import Message from "./Message.vue";
import Popup from "./Popup.vue";

import axios from "axios";
axios.defaults.xsrfCookieName = "csrftoken";
axios.defaults.xsrfHeaderName = "X-CSRFToken";
//const base_url = window.location.href;

export default {
  name: "Chat",
  components: {
    Message,
    Popup,
  },
  data: () => ({
    chat: [],
    msg: null,
    items: ["context", "image", "audio"],
  }),
  mounted: function () {
    this.addImage("kiyoung2", require("../../assets/image/kiyoung2.png"));
    this.addReply("안녕! 반가워😍 나는 기영이라고 해~");
    this.addReply("모르는게 있으면 물어봐!");
    this.addReply("나 꽤나 똑똑하다고~");
  },
  methods: {
    send: async function () {
      this.chat.push({
        from: "user",
        msg: this.msg,
        img: null,
      });
      const payload = { question: this.msg };
      const url = "http://127.0.0.1:5000/answer-question";
      const headers = {
        "Content-Type": "application/json",
      };

      this.msg = null;
      await axios.post(url, payload, { headers: headers }).then((response) => {
        console.log(response.data);
        this.answer = response.data;
        this.answer.forEach(function (element, index) {
          if (index == 0) {
            this.addReply(element);
          } else {
            setTimeout(this.addReply, 1000, element);
          }
        }, this);
      });
    },
    addReply(msg) {
      this.chat.push({
        from: "kiyoung2",
        msg: msg,
        img: null,
      });
    },
    addImage(from, img_src) {
      this.chat.push({
        from: from,
        msg: null,
        img: img_src,
      });
    },
  },
};
</script>