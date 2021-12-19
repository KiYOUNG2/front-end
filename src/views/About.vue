<template>
  <v-container fluid>
    <h1>팀 기영이를 소개합니다!</h1>
    <v-row>
      <v-col
        v-for="(person, i) in people"
        :key="i"
        class="d-flex child-flex"
        cols="1.5"
      >
        <v-row class="flex-column">
          <v-col>
            <span style="font-size: large">{{ person.name }}</span>
          </v-col>
          <v-col>
            <v-img
              :src="person.img_src"
              aspect-ratio="1"
              class="grey lighten-2"
            >
            </v-img>
          </v-col>
          <v-col>
            <a :href="person.github" target="_blank">
              <span>GitHub</span>
            </a>
          </v-col>
        </v-row>
      </v-col>
    </v-row>
    <v-timeline>
      <v-timeline-item
        v-for="(item, i) in items"
        :key="i"
        :color="item.color"
        small
      >
        <template v-slot:opposite>
          <span
            :class="`font-weight-bold ${item.color}--text`"
            v-text="item.period"
          ></span>
        </template>
        <div class="py-4">
          <v-card :color="item.color">
            <v-expansion-panels>
              <v-expansion-panel
                @click="item.color = item.color == 'grey' ? 'black' : 'grey'"
              >
                <v-expansion-panel-header>
                  <span
                    style="font-size: x-large"
                    :style="`color: ${item.color}`"
                  >
                    {{ item.title }}
                  </span>
                </v-expansion-panel-header>
                <v-expansion-panel-content>
                  <a :href="item.link" target="_blank">
                    <v-img :src="item.img_src"> </v-img>
                  </a>
                  <span>{{ item.description }}</span>
                </v-expansion-panel-content>
              </v-expansion-panel>
            </v-expansion-panels>
          </v-card>
        </div>
      </v-timeline-item>
    </v-timeline>
  </v-container>
</template>

<script>
export default {
  name: "About",
  data: () => ({
    items: [
      {
        title: "문장 내 개체간 관계 추출(RE) 대회 🥇",
        color: "grey",
        period: "2021.09.27 ~ 2021.10.07 (2주)",
        img_src: require("@/assets/image/klue_re.png"),
        link: "https://github.com/boostcampaitech2/klue-level2-nlp-14",
        description: "👆 기영이가 어떻게 1위 했는지 궁금하다면 클릭! 👆",
      },
      {
        title: "오픈 도메인 질의응답(ODQA) 대회 🥇",
        color: "grey",
        period: "2021.10.12 ~ 2021.11.04 (4주)",
        img_src: require("@/assets/image/odqa.png"),
        link: "https://github.com/boostcampaitech2/mrc-level2-nlp-14",
        description: "👆 기영이가 어떻게 1위 했는지 궁금하다면 클릭! 👆",
      },
      {
        title: "관계 추출 데이터 제작 및 검증",
        color: "grey",
        period: "2021.11.08 ~ 2021.11.19 (2주)",
        img_src: require("@/assets/image/data_annotation.png"),
        link: "https://github.com/boostcampaitech2/data-annotation-nlp-level3-nlp-14",
        description: "👆 기영이가 제작한 데이터가 궁금하다면 클릭! 👆",
      },
      {
        title: "이미지 분류 모델 경량화 대회",
        color: "grey",
        period: "2021.11.22 ~ 2021.12.02 (2주)",
        img_src: require("@/assets/image/optimization.png"),
        link: "https://github.com/boostcampaitech2/model-optimization-level3-nlp-14",
        description: "👆 기영이가 어떻게 진행했는지 궁금하다면 클릭! 👆",
      },
      {
        title: "최종 프로젝트 기영이봇",
        color: "grey",
        period: "2021.11.08 ~ 2021.12.22 (6~7주)",
        img_src: require("@/assets/image/profile_kiyoung.png"),
        link: "https://github.com/KiYOUNG2",
        description: "👆 기영이봇이 어떻게 만들어졌는지 궁금하다면 클릭! 👆",
      },
    ],
    people: [
      {
        name: "김대웅",
        img_src: "https://avatars.githubusercontent.com/u/41335296?v=4",
        github: "https://github.com/KimDaeUng",
      },
      {
        name: "김채은",
        img_src: "https://avatars.githubusercontent.com/u/60843683?v=4",
        github: "https://github.com/Amber-Chaeeunk",
      },
      {
        name: "김태욱",
        img_src: "https://avatars.githubusercontent.com/u/47404628?v=4",
        github: "https://github.com/taeukkkim",
      },
      {
        name: "유영재",
        img_src: "https://avatars.githubusercontent.com/u/53523319?v=4",
        github: "https://github.com/uyeongjae",
      },
      {
        name: "이하람",
        img_src: "https://avatars.githubusercontent.com/u/35680202?v=4",
        github: "https://github.com/hrxorxm",
      },
      {
        name: "진명훈",
        img_src: "https://avatars.githubusercontent.com/u/37775784?v=4",
        github: "https://github.com/jinmang2",
      },
      {
        name: "허진규",
        img_src: "https://avatars.githubusercontent.com/u/88299729?v=4",
        github: "https://github.com/JeangyuHeo",
      },
    ],
  }),
};
</script>