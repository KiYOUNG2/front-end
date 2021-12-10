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
      <v-list-item>
        <div class="text-xs-center">
          <v-tooltip right max-width="250">
            <template v-slot:activator="{ on }">
              <v-btn color="black" dark v-on="on">Document</v-btn>
            </template>
            <span>질문에 필요한 document를 선택하세요. 최대 5개까지 업로드 가능하며 중복하여 선택할 수 있습니다.</span>
          </v-tooltip>
          <ContextSelector />
          <v-tooltip right max-width="250">
            <template v-slot:activator="{ on }">
              <v-btn color="black" dark v-on="on">Image</v-btn>
            </template>
            <span>질문에 필요한 Image를 선택하세요. 최대 5개까지 업로드 가능하며 중복하여 선택할 수 없습니다.</span>
          </v-tooltip>
          <ImageSelector />
        </div>
      </v-list-item>
    </v-list>
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
  }),
};
</script>

<style lang="sass" scoped>
.v-card.on-hover.theme--dark
  background-color: rgba(#FFF, 0.8)
  >.v-card__text
    color: #000
</style>