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
import Message from "./Message.vue";
import Popup from "./Popup.vue";
import eventBus from "../../main.js";

import axios from "axios";
axios.defaults.xsrfCookieName = "csrftoken";
axios.defaults.xsrfHeaderName = "X-CSRFToken";

export default {
  name: "Chat",
  components: {
    Message,
    Popup,
  },
  data: () => ({
    chat: [],
    user_name: "user",
    bot_name: "kiyoung2",
    msg: null,
    context_type: null,
    image: null,
    document: null,
  }),
  mounted: function () {
    this.addImage(this.bot_name, require("../../assets/image/kiyoung2.png"));
    this.addMessage(this.bot_name, "안녕! 반가워😍 나는 기영이라고 해~");
    this.addMessage(this.bot_name, "모르는게 있으면 물어봐!");
    this.addMessage(this.bot_name, "나 꽤나 똑똑하다고~");
  },
  created() {
    eventBus.$on("context", (type, context) => {
      this.context_type = type;
      if (this.context_type == "image") {
        this.image = context;
        this.document = null;
        if (this.image != null) {
          const img_src = window.URL.createObjectURL(this.image);
          this.addImage(this.user_name, img_src);
        }
      } else {
        this.image = null;
        this.document = "";
        context.forEach((element) => {
          this.addMessage(this.user_name, element);
          this.document += element + " ";
        });
      }
    });
  },
  methods: {
    send: async function () {
      this.addMessage(this.user_name, this.msg);
      const payload = {
        question: this.msg,
        knowledge: this.knowledge_cache.find(
          (v) => v.name == this.knowledge_name
        ),
      };
      const url = "http://127.0.0.1:5000/answer-question";
      const headers = {
        "Content-Type": "application/json",
      };
      this.msg = null;
      this.knowledge_name = null;
      await axios.post(url, payload, { headers: headers }).then((response) => {
        console.log(response.data);
        this.answer = response.data;
        this.answer.forEach(function (element) {
          this.addMessage(this.bot_name, element);
        }, this);
      });
    },
    addMessage(from, msg) {
      this.chat.push({
        from: from,
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