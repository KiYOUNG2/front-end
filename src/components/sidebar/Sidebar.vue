<template>
  <v-container>
    <v-list-item>
      <v-list-item-avatar>
        <v-img src="../../assets/image/kiyoung2.png"></v-img>
      </v-list-item-avatar>
      <v-list-item-content>
        <v-list-item-title style="font-size: 25px"
          >Kiyoung2Bot</v-list-item-title
        >
      </v-list-item-content>
    </v-list-item>
    <v-divider></v-divider>
    <div class="text-xs-center">
      <v-tooltip right max-width="250">
        <template v-slot:activator="{ on, attrs }">
          <span v-bind="attrs" v-on="on" style="font: italic bold 1.2em/1em Georgia, serif">Documents</span>
        </template>
        <span
          >질문에 필요한 document를 선택하세요. 최대 5개까지 업로드
          가능합니다.</span
        >
      </v-tooltip>
      <ContextSelector />
      <v-tooltip right max-width="250">
        <template v-slot:activator="{ on, attrs }">
          <span v-bind="attrs" v-on="on" style="font: italic bold 1.2em/1em Georgia, serif">Image</span>
        </template>
        <span
          >질문에 필요한 Image를 선택하세요. 최대 5개까지 업로드
          가능합니다.</span
        >
      </v-tooltip>
      <ImageSelector />
    </div>
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
  data: () => ({}),
};
</script>

<style lang="sass" scoped>
.v-card.on-hover.theme--dark
  background-color: rgba(#FFF, 0.8)
  >.v-card__text
    color: #000
</style>