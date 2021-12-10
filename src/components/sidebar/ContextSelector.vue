<template>
  <v-container dense>
    <v-row class="mt-12">
      <v-checkbox
        :disabled="get_image != null"
        label="Context 1"
        color="amber accent-2"
        hide-details
      >
      </v-checkbox>
      <v-checkbox
        :disabled="get_image != null"
        label="Context 2"
        color="amber accent-2"
        hide-details
      >
      </v-checkbox>
      <v-checkbox
        :disabled="get_image != null"
        label="Context 3"
        color="amber accent-2"
        hide-details
      >
      </v-checkbox>
      <v-checkbox
        :disabled="get_image != null"
        label="Context 4"
        color="amber accent-2"
        hide-details
      >
      </v-checkbox>
    </v-row>
  </v-container>
</template>

<script>
import Vue from "vue";
var eventBus = new Vue();

export default {
  name: "ContextSelector",
  data: () => ({
    get_image: null,
  }),
  created() {
    eventBus.$on("file", (file) => {
      this.get_image = file;
    });
  },
};
</script>