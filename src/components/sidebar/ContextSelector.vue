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
    <span v-html="show"> </span>
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
    show_context: "",
  }),
  created() {
    eventBus.$on("context", (type) => {
      if (type == "image") {
        this.highlight.backgroundColor = "#ffffff";
      } else {
        this.highlight.backgroundColor = "#ffe57f";
      }
    });
    eventBus.$on("doc_cache", (documents) => {
      this.doc_cache = documents;
      this.value = [this.doc_cache[this.doc_cache.length - 1]];
      this.send_context();
    });
  },
  computed: {
    show() {
      return this.show_context.replace("\n", "<br />");
    },
  },
  methods: {
    select_context() {
      this.send_context();
      this.highlight.backgroundColor = "#ffe57f";
    },
    send_context() {
      eventBus.$emit("context", "document", this.value);
      this.show_context = "";
      this.value.forEach((element) => {
        this.show_context += element + "\n";
      });
    },
  },
};
</script>