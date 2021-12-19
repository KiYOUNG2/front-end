<template>
  <v-container>
    <section
      style="height: 600px; overflow-y: auto; overflow-x: hidden"
      ref="messagesContainer"
    >
      <div
        align="end"
        style="padding: 1%"
        v-for="(item, index) in chat"
        :key="index"
        :class="[
          'd-flex flex-row my-2',
          item.from == '바트' ? 'justify-end' : null,
        ]"
      >
        <v-row class="flex-column" v-if="item.from == '바트'">
          <v-col :class="['d-flex child-flex', 'justify-end']">
            <span style="text-align: end;">{{
              item.from
            }}</span>
          </v-col>
          <v-col :class="['d-flex', 'justify-end']">
            <span
              v-if="item.msg != null"
              style="
                display: inline-flex;
                font-size: large;
                max-width: 60%;
                text-align: right;
                border-radius: 10px;
                padding: 0.5em;
                background: #ffe57f;
                color: black;
              "
              >{{ item.msg }}</span
            >
            <ZoomImage v-if="item.img != null" v-bind:item="item" />
          </v-col>
        </v-row>
        <v-col cols="1">
          <v-avatar
            :color="item.from == '바트' ? 'grey' : 'amber accent-2'"
            size="50"
          >
            <v-img :src="getProfileImage(item.from)"></v-img>
          </v-avatar>
        </v-col>
        <v-row class="flex-column" v-if="item.from != '바트'">
          <v-col class="d-flex child-flex">
            <span
              style="text-align: left"
              >{{ item.from }}</span
            >
          </v-col>
          <v-col class="d-flex">
            <span
              v-if="item.msg != null"
              style="
                display: inline-flex;
                font-size: large;
                max-width: 60%;
                text-align: left;
                border-radius: 10px;
                padding: 0.5em;
                background: #f1f0f0;
                color: black;
              "
              >{{ item.msg }}</span
            >
            <ZoomImage v-if="item.img != null" v-bind:item="item" />
          </v-col>
        </v-row>
      </div>
    </section>
  </v-container>
</template>

<script>
import ZoomImage from "./ZoomImage.vue";

export default {
  name: "Message",
  components: {
    ZoomImage,
  },
  props: ["chat"],
  updated() {
    this.$nextTick(() => this.scrollToEnd());
  },
  methods: {
    getProfileImage(from) {
      if (from == "바트") {
        return require("@/assets/image/profile_bart.png");
      } else {
        return require("@/assets/image/profile_kiyoung.png");
      }
    },
    scrollToEnd: function () {
      var content = this.$refs.messagesContainer;
      content.scrollTop = content.scrollHeight;
    },
  },
};
</script>