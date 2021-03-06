<template>
  <v-dialog transition="dialog-bottom-transition" max-width="600" scrollable>
    <template v-slot:activator="{ on, attrs }">
      <v-btn class="mx-2" fab dark small color="black" v-bind="attrs" v-on="on">
        <v-icon dark>mdi-plus</v-icon>
      </v-btn>
    </template>
    <!-- 팝업창 -->
    <template v-slot:default="dialog">
      <v-card>
        <v-toolbar color="black" dark flat>
          <v-toolbar-title>Write a document or upload a file</v-toolbar-title>
          <template v-slot:extension>
            <v-tabs v-model="tabs" centered>
              <v-tabs-slider color="grey darken-2"></v-tabs-slider>
              <v-tab>text</v-tab>
              <v-tab>file</v-tab>
            </v-tabs>
          </template>
        </v-toolbar>
        <v-tabs-items v-model="tabs">
          <v-tab-item>
            <v-card flat>
              <v-form ref="form" @submit.prevent="submit">
                <v-container fluid>
                  <v-row>
                    <v-col cols="12">
                      <v-textarea
                        v-model="document"
                        color="black"
                        maxlength="1000"
                      >
                        <template v-slot:label>
                          <div>Write a document</div>
                        </template>
                      </v-textarea>
                    </v-col>
                  </v-row>
                </v-container>
                <v-card-actions>
                  <v-btn text @click="dialog.value = false">Close</v-btn>
                  <v-spacer></v-spacer>
                  <v-btn
                    :disabled="!DocumentIsValid"
                    text
                    color="black"
                    type="submit"
                    @click="
                      uploadText(document);
                      dialog.value = false;
                    "
                  >
                    Upload
                  </v-btn>
                </v-card-actions>
              </v-form>
            </v-card>
          </v-tab-item>
          <v-tab-item>
            <v-card flat>
              <v-form ref="form" @submit.prevent="submit">
                <v-container fluid>
                  <v-row>
                    <v-col cols="12">
                      <v-file-input
                        v-model="file"
                        :rules="rules"
                        accept="image/png, image/jpeg, image/jpg, .doc, .txt"
                        placeholder="Pick an file"
                        prepend-icon="mdi-paperclip"
                        label="File"
                      >
                      </v-file-input>
                    </v-col>
                  </v-row>
                </v-container>
                <v-card-actions>
                  <v-btn text @click="dialog.value = false">Close </v-btn>
                  <v-spacer></v-spacer>
                  <v-btn
                    :disabled="FileIsValid == null"
                    text
                    color="black"
                    type="submit"
                    @click="
                      uploadFile(file);
                      dialog.value = false;
                    "
                  >
                    Upload
                  </v-btn>
                </v-card-actions>
              </v-form>
            </v-card>
          </v-tab-item>
        </v-tabs-items>
      </v-card>
    </template>
  </v-dialog>
</template>

<script>
import eventBus from "../../main.js";

export default {
  name: "Popup",
  computed: {
    DocumentIsValid() {
      return this.document;
    },
    FileIsValid() {
      return this.file;
    },
  },
  data: () => ({
    tabs: null,
    document: "",
    documents: [],
    file: null,
    files: [],
    rules: [
      (value) =>
        !value ||
        value.size < 10000000 ||
        "File size should be less than 10 MB!",
    ],
  }),
  methods: {
    resetKnowledge() {
      this.document = "";
      this.file = null;
    },
    submit() {
      this.resetKnowledge();
    },
    uploadFile(file) {
      if (file.type.startsWith("image/")) {
        this.files.push(file);
        eventBus.$emit("img_cache", this.files);
        this.$emit('uploaded', "이미지");
      } else {
        const reader = new FileReader();
        reader.onload = (e) => {
          this.uploadText(e.target.result);
        };
        reader.readAsText(file);
      }
    },
    uploadText(document) {
      this.documents.push(document);
      eventBus.$emit("doc_cache", this.documents);
      this.$emit('uploaded', "문서");
    },
  },
};
</script>