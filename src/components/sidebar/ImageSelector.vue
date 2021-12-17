<template>
  <v-container dense :style="highlight">
    <v-autocomplete
      v-model="value"
      :data="value"
      :items="img_cache_names"
      dense
      solo
      filled
      clearable
      deletable-chips
      label="Select an image"
      @change="select_context()"
    ></v-autocomplete>
  </v-container>
</template>

<script>
import eventBus from "../../main.js";

export default {
  name: "ImageSelector",
  data: () => ({
    img_cache: [],
    img_cache_names: [],
    value: null,
    highlight: {
    backgroundColor: "#ffffff",
    },
  }),
  created() {
    eventBus.$on("context", (type) => {
      if (type == "document") {
        this.highlight.backgroundColor = "#ffffff";
      } else {
        this.highlight.backgroundColor = "#f0f4c3";
      }
    });
    eventBus.$on("img_cache", (files) => {
      this.img_cache = files;
      this.img_cache_names = [];
      this.img_cache.forEach((element) => {
        this.img_cache_names.push(element.name);
      });
      this.value = this.img_cache_names[this.img_cache_names.length - 1];
      this.send_context();
    });
  },
  methods: {
    select_context() {
      this.send_context();
      this.highlight.backgroundColor = "#f0f4c3";
    },
    send_context() {
      if (this.value == null) {
        eventBus.$emit("context", "image", null);
      } else {
        this.img_cache.forEach((element) => {
          if (element.name == this.value) {
            eventBus.$emit("context", "image", element);
          }
        });
      }
    },
  },
};
</script>