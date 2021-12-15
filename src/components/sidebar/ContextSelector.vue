<template>
  <v-container dense :style="highlight">
    <v-autocomplete
      v-model="value"
      :data="value"
      :items="doc_cache"
      multiple
      dense
      solo
      filled
      clearable
      deletable-chips
      label="Select the documents"
      @change="select_context()"
    ></v-autocomplete>
  </v-container>
</template>

<script>
import eventBus from "../../main.js";

export default {
  name: "ContextSelector",
  data: () => ({
    doc_cache: [],
    value: null,
    highlight: {
      backgroundColor: "#ffffff",
    },
  }),
  created() {
    eventBus.$on("context", (type) => {
      if (type == "image") {
        this.highlight.backgroundColor = "#ffffff";
      } else {
        this.highlight.backgroundColor = "#f0f4c3";
      }
    });
    eventBus.$on("doc_cache", (documents) => {
      this.doc_cache = documents;
      this.value = [this.doc_cache[this.doc_cache.length - 1]];
      this.send_context();
    });
  },
  methods: {
    select_context() {
      this.send_context();
      this.highlight.backgroundColor = "#f0f4c3";
    },
    send_context() {
      eventBus.$emit("context", "document", this.value);
    },
  },
};
</script>