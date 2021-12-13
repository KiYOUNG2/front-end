<template>
  <v-container dense>
    <v-row class="mt-12">
      <v-checkbox v-model="checkbox"
        label="Image 1"
        color="amber accent-2"
        hide-details
        value="Image 1"
      >
      </v-checkbox>
      <v-checkbox v-model="checkbox"
        label="Image 2"
        color="amber accent-2"
        hide-details
        value="Image 2"
      >
      </v-checkbox>
      <v-checkbox v-model="checkbox"
        label="Image 3"
        color="amber accent-2"
        hide-details
        value="Image 3"
      >
      </v-checkbox>
      <v-checkbox v-model="checkbox"
        label="Image 4"
        color="amber accent-2"
        hide-details
        value="Image 4"
      >
      </v-checkbox>
      <v-checkbox v-model="checkbox"
        label="Image 5"
        color="amber accent-2"
        hide-details
        value="Image 5"
      >
      </v-checkbox>
    </v-row>
    <div class="my-2">
      <v-btn
        :disabled="this.get_context != null"
        small
        color="grey-1"
        dark
        @click="get_image(checkbox)"
      >
        Select
      </v-btn>
    </div>
  </v-container>
</template>



<script>
import eventBus from '../../main.js'

export default {
  name: "ImageSelector",
  data: () => ({
    radioGroup: 1,
    get_context: null,
    checkbox : null,
  }),
  created() {
    eventBus.$on("get_context", function(checkbox) {
      this.get_context = checkbox
    })
  },
  methods: {
    get_image(checkbox) {
      eventBus.$emit("get_image", checkbox);
    },
  }
};
</script>