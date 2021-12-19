<template>
  <v-app app>
    <!-- 사이드 바 -->
    <v-navigation-drawer v-model="drawer" absolute temporary width="20%">
      <Sidebar />
    </v-navigation-drawer>
    <!-- 앱 상단 바 -->
    <v-app-bar app color="amber accent-2" flat>
      <v-btn icon @click.stop="drawer = !drawer">
        <v-icon>mdi-chevron-right</v-icon>
      </v-btn>
      <v-container class="py-0 fill-height">
        <v-btn text class="font-weight-bold">
          <router-link to="/" style="text-decoration: none; color: black"
            >Kiyoung2BOT</router-link
          >
        </v-btn>
        <v-btn text class="font-weight-bold">
          <router-link to="/about" style="text-decoration: none; color: black"
            >About us</router-link
          >
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
        <v-btn icon>
          <v-icon>mdi-magnify</v-icon>
        </v-btn>
      </v-container>
    </v-app-bar>
    <!-- 메인 컨텐츠 (봇) -->
    <v-main class="grey lighten-3">
      <router-view></router-view>
    </v-main>
  </v-app>
</template>

<script>
import Sidebar from "./components/sidebar/Sidebar.vue";

export default {
  name: "App",
  components: {
    Sidebar,
  },
  data() {
    return {
      drawer: null,
    };
  },
};
</script>

<style>
@import "//unpkg.com/bootstrap/dist/css/bootstrap.min.css";
@import "//unpkg.com/bootstrap-vue@latest/dist/bootstrap-vue.min.css";
@import url("https://fonts.googleapis.com/css2?family=Gowun+Dodum&display=swap");

h1,
div,
span {
  font-family: "Gowun Dodum", sans-serif;
  text-align: center;
}
</style>