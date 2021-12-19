<template>
  <v-container>
    <section
      style="height: 400px; overflow-y: auto; overflow-x: hidden"
      ref="messagesContainer"
    >
      <div
        align="end"
        style="padding: 1%"
        v-for="(item, index) in chat"
        :key="index"
        :class="[
          'd-flex flex-row my-2',
          item.from == 'user' ? 'justify-end' : null,
        ]"
      >
        <v-row class="flex-column" v-if="item.from == 'user'">
          <v-col :class="['d-flex child-flex', 'justify-end']">
            <span style="font-family: 'Roboto Slab', serif">{{
              item.from
            }}</span>
          </v-col>
          <v-col :class="['d-flex', 'justify-end']">
            <span
              v-if="item.msg != null"
              style="
                font-family: 'Gamja Flower', cursive;
                font-size: x-large;
                max-width: 60%;
                text-align: right;
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
        <v-col cols="1">
          <v-avatar
            :color="item.from == 'user' ? 'grey' : 'amber accent-2'"
            size="50"
          >
            <v-img :src="getProfileImage(item.from)"></v-img>
          </v-avatar>
        </v-col>
        <v-row class="flex-column" v-if="item.from != 'user'">
          <v-col class="d-flex child-flex">
            <span style="font-family: 'Roboto Slab', serif; text-align: left">{{
              item.from
            }}</span>
          </v-col>
          <v-col class="d-flex">
            <span
              v-if="item.msg != null"
              style="
                font-family: 'Gamja Flower', cursive;
                font-size: x-large;
                max-width: 60%;
                text-align: left;
                border-radius: 10px;
                padding: 0.5em;
                background: #ffc400;
                color: white;
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
      if (from == "user") {
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

<style>
@import url("https://fonts.googleapis.com/css2?family=Gamja+Flower&display=swap");
@import url("https://fonts.googleapis.com/css2?family=Roboto+Slab&display=swap");
</style>