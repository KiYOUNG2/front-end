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
                  <Popup />
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
import Message from './Message.vue';
import Popup from './Popup.vue';

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
    this.addReply("안녕하세요! 기영이 봇 입니다~");
    this.addReply("무엇이 궁금하신가요?");
  },
  methods: {
    send: async function () {
      this.chat.push({
        from: "user",
        msg: this.msg,
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
        this.answer.forEach(function (element) {
          this.addReply(element);
        }, this);
      });
    },
    addReply(msg) {
      this.chat.push({
        from: "kiyoung2",
        msg: msg,
      });
    },
  },
};
</script>