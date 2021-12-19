<template>
  <v-container>
    <v-timeline>
      <v-timeline-item
        v-for="(year, i) in years"
        :key="i"
        :color="year.color"
        small
      >
        <template v-slot:opposite>
          <span
            :class="`headline font-weight-bold ${year.color}--text`"
            v-text="year.year"
          ></span>
        </template>
        <div class="py-4">
          <h2 :class="`headline font-weight-bold ${year.color}--text`">
            {{ year.title }}
          </h2>
          <v-expansion-panels popout>
            <v-expansion-panel>
              <v-expansion-panel-header> Item </v-expansion-panel-header>
              <v-expansion-panel-content>
                Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do
                eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut
                enim ad minim veniam, quis nostrud exercitation ullamco laboris
                nisi ut aliquip ex ea commodo consequat.
              </v-expansion-panel-content>
            </v-expansion-panel>
          </v-expansion-panels>
        </div>
      </v-timeline-item>
    </v-timeline>
  </v-container>
</template>

<script>
export default {
  name: "About",
  data: () => ({
    years: [
      {
        title: "Relation Extraction 대회 1등",
        color: "cyan",
        year: "2021.00.00 ~ 2021.00.00",
      },
      {
        title: "Open Domain Question Answering 대회 1등",
        color: "green",
        year: "2021.00.00 ~ 2021.00.00",
      },
      {
        title: "데이터 제작 PRED",
        color: "pink",
        year: "2021.00.00 ~ 2021.00.00",
      },
      {
        title: "모델 경량화 대회",
        color: "amber",
        year: "2021.00.00 ~ 2021.00.00",
      },
      {
        title: "읽거나 보고, 아는 것만 답변하는 지혜로운 기영이봇",
        color: "orange",
        year: "2021.00.00 ~ 2021.00.00",
      },
    ],
  }),
};
</script>