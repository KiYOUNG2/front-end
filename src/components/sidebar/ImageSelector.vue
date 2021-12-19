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
    <v-img
        style="max-width: 100%;"
        :src="img_src"
        v-bind="attrs"
        v-on="on"
      >
  </v-img>
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
    img_src : null,
    },
  }),
  created() {
    eventBus.$on("context", (type) => {
      if (type == "document") {
        this.highlight.backgroundColor = "#ffffff";
      } else {
        this.highlight.backgroundColor = "#ffe57f";
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
      this.highlight.backgroundColor = "#ffe57f";
    },
    send_context() {
      if (this.value == null) {
        eventBus.$emit("context", "image", null);
      } else {
        this.img_cache.forEach((element) => {
          if (element.name == this.value) {
            this.img_src = window.URL.createObjectURL(element)
            eventBus.$emit("context", "image", element);
          }
        });
      }
    },
  },
};
</script>