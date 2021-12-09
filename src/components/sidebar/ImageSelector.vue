<template>
  <v-container dense>
    <v-radio-group v-model="radioGroup">
      <v-radio
        v-for="n in 3"
        :key="n"
        :label="`Image ${n}`"
        :value="n"
        color="amber accent-2"
      ></v-radio>
    </v-radio-group>
  </v-container>
</template>

<script>
import Vue from "vue";
var eventBus = new Vue();

export default {
  name: "ImageSelector",
  data: () => ({
    radioGroup: 1,
    get_context: null,
  }),
  created() {
    eventBus.$on("context", (context) => {
      this.get_context = context;
    });
  },
};
</script>