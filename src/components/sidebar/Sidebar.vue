<template>
  <v-container>
    <div class="text-xs-center">
      <v-col class="ml-auto">
        <v-tooltip right max-width="250">
          <template v-slot:activator="{ on, attrs }">
            <span
              v-bind="attrs"
              v-on="on"
              style="font-size: large; font-weight: bold"
              >문서 선택하기</span
            >
          </template>
          <span
            >질문에 필요한 document를 선택하세요. 최대 5개까지 업로드
            가능합니다.</span
          >
        </v-tooltip>
        <ContextSelector />
      </v-col>
      <v-col class="ml-auto">
        <v-tooltip right max-width="250">
          <template v-slot:activator="{ on, attrs }">
            <span
              v-bind="attrs"
              v-on="on"
              style="font-size: large; font-weight: bold"
              >이미지 선택하기</span
            >
          </template>
          <span
            >질문에 필요한 Image를 선택하세요. 최대 5개까지 업로드
            가능합니다.</span
          >
        </v-tooltip>
        <ImageSelector />
      </v-col>
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
};
</script>

<style lang="sass" scoped>
.v-card.on-hover.theme--dark
  background-color: rgba(#FFF, 0.8)
  >.v-card__text
    color: #000
</style>