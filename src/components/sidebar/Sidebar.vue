<template>
  <v-container>
    <v-list-item>
      <v-list-item-avatar>
        <v-img src="../../assets/image/kiyoung2.png"></v-img>
      </v-list-item-avatar>
      <v-list-item-content>
        <v-list-item-title style="font-size: 20px">기영이봇</v-list-item-title>
      </v-list-item-content>
    </v-list-item>
    <v-divider></v-divider>
    <v-list dense>
      <v-list-item v-for="menu in menus" :key="menu.title" link>
        <v-list-item-icon>
          <v-icon>{{ menu.icon }}</v-icon>
        </v-list-item-icon>

        <v-list-item-content>
          <v-list-item-title>{{ menu.title }}</v-list-item-title>
        </v-list-item-content>
      </v-list-item>
    </v-list>
    <ImageSelector />
    <ContextSelector />
  </v-container>
</template>

<script>
import ImageSelector from "./ImageSelector.vue";
import ContextSelector from "./ContextSelector.vue";

export default {
  name: "Sidebar",
  components: {
    ImageSelector,
    ContextSelector,
  },
  data: () => ({
    menus: [
      { title: "Home", icon: "mdi-view-dashboard" },
      { title: "About", icon: "mdi-forum" },
    ],
  }),
};
</script>
