<template>
  <v-container dense>
    <v-row class="mt-12">
      <v-checkbox v-model="checkbox"
        label="Context 1"
        color="amber accent-2"
        hide-details
        value="Context 1"
      >
      </v-checkbox>
      <v-checkbox v-model="checkbox"
        label="Context 2"
        color="amber accent-2"
        hide-details
        value="Context 2"
      >
      </v-checkbox>
      <v-checkbox v-model="checkbox"
        label="Context 3"
        color="amber accent-2"
        hide-details
        value="Context 3"
      >
      </v-checkbox>
      <v-checkbox v-model="checkbox"
        label="Context 4"
        color="amber accent-2"
        hide-details
        value="Context 4"
      >
      </v-checkbox>
      <v-checkbox v-model="checkbox"
        label="Context 5"
        color="amber accent-2"
        hide-details
        value="Context 5"
      >
      </v-checkbox>
    </v-row>
    <div class="my-2">
      <v-btn
        :disabled="this.get_image != null"
        small
        color="grey-1"
        dark
        @click="get_context(checkbox)"
      >
        Select
      </v-btn>
    </div>
  </v-container>
</template>

<script>
import eventBus from '../../main.js'

export default {
  name: "ContextSelector",
  data: () => ({
    get_image: null,
    checkbox: null,
  }),
  created() {
    eventBus.$on("get_image", function(checkbox) {
      this.get_image = checkbox;
    });
  },
  methods: {
    get_context(checkbox) {
      eventBus.$emit("get_context", checkbox)
    }
  }
};
</script>