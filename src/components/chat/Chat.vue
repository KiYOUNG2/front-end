<template>
  <v-container style="width: 80%;">
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
                  <Popup v-on:uploaded="openSnackbar($event)" />
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
    <v-snackbar v-model="snackbar" :timeout="timeout" color="amber darken-1">
      <span style="color: black">
        {{ text }}
      </span>
    </v-snackbar>
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
    user_name: "바트",
    bot_name: "기영이",
    msg: null,
    context_type: null,
    image: null,
    document: null,
    snackbar: false,
    text: "업로드 완료 메세지",
    timeout: 3000,
  }),
  mounted: function () {
    this.addImage(this.bot_name, require("../../assets/image/kiyoung2.png"));
    setTimeout(this.addMessage, 1000, this.bot_name, "안녕! 반가워😍 나는 기영이라고 해~");
    setTimeout(this.addMessage, 2000, this.bot_name, "모르는게 있으면 물어봐!");
    setTimeout(this.addMessage, 3000, this.bot_name, "나 꽤나 똑똑하다고~");
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
          this.document += element + " ";
        });
      }
    });
  },
  methods: {
    send: async function () {
      if (this.msg === null) {
        return;
      }
      this.addMessage(this.user_name, this.msg);
      let formData = new FormData();
      formData.append("query", this.msg);
      formData.append("document", this.document === null ? "" : this.document);
      formData.append("image", this.image === null ? "" : this.image);

      const url = "http://localhost:8000/api/chat";
      const headers = {
        "Content-Type": "multipart/form-data",
      };
      this.msg = null;
      await axios.post(url, formData, { headers: headers }).then((response) => {
        this.answer = response.data;
        this.answer.forEach(function (element, index) {
          if (element != "") {
            if (index == 0) {
              this.addMessage(this.bot_name, element);
            } else {
              setTimeout(this.addMessage, 1000, this.bot_name, element);
            }
          }
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
    openSnackbar(context) {
      this.text = `📢 ${context}가 성공적으로 추가되었습니다.`;
      this.snackbar = true;
    },
  },
};
</script>