<template>
  <v-app app>
    <!-- 사이드 바 -->
    <v-navigation-drawer v-model="drawer" absolute temporary>
      <Sidebar />
    </v-navigation-drawer>
    <!-- 앱 상단 바 -->
    <v-app-bar app color="amber accent-2" flat>
      <v-btn icon @click.stop="drawer = !drawer">
        <v-icon>mdi-chevron-right</v-icon>
      </v-btn>
      <v-container class="py-0 fill-height">
        <v-avatar class="mr-10" color="black" size="32"></v-avatar>
        <v-btn v-for="link in links" :key="link" text>
          {{ link }}
        </v-btn>
        <v-spacer></v-spacer>
        <v-responsive max-width="260">
          <v-text-field
            dense
            flat
            hide-details
            rounded
            solo-inverted
          ></v-text-field>
        </v-responsive>
      </v-container>
    </v-app-bar>
    <!-- 메인 컨텐츠 (봇) -->
    <v-main class="grey lighten-3">
      <Chat />
    </v-main>
  </v-app>
</template>

<script>
import Sidebar from "./components/sidebar/Sidebar.vue";
import Chat from "./components/chat/Chat.vue";

export default {
  name: "App",
  components: {
    Chat,
    Sidebar,
  },
  data() {
    return {
      drawer: null,
      links: ["Home", "Kiyoung2BOT", "About us"],
    };
  },
};
</script>

<style>
@import "//unpkg.com/bootstrap/dist/css/bootstrap.min.css";
@import "//unpkg.com/bootstrap-vue@latest/dist/bootstrap-vue.min.css";
</style>