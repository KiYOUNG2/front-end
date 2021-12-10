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
          <v-toolbar-title>Upload documents or images</v-toolbar-title>
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
              <v-snackbar v-model="snackbar" absolute top right color="success">
                <span>Upload successful!</span>
                <v-icon dark> mdi-checkbox-marked-circle </v-icon>
              </v-snackbar>
              <v-form ref="form" @submit.prevent="submit">
                <v-container fluid>
                  <v-row>
                    <v-col cols="12">
                      <v-textarea
                        v-model="context"
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
                    :disabled="!ContextIsValid"
                    text
                    color="black"
                    type="submit"
                    @click="uploadText(context)"
                  >
                    Upload
                  </v-btn>
                </v-card-actions>
              </v-form>
            </v-card>
          </v-tab-item>
          <v-tab-item>
            <v-card flat>
              <v-snackbar v-model="snackbar" absolute top right color="success">
                <span>Upload successful!</span>
                <v-icon dark> mdi-checkbox-marked-circle </v-icon>
              </v-snackbar>
              <v-form ref="form" @submit.prevent="submit">
                <v-container fluid>
                  <v-row>
                    <v-col cols="12">
                      <v-file-input
                        v-model="file"
                        :rules="rules"
                        accept="image/png, image/jpeg, image/bmp, audio/wav, video/mp4"
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
                    :disabled="FileIsValid==null"
                    text
                    color="black"
                    type="submit"
                    @click="uploadFile(file)"
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
import Vue from "vue";
var eventBus = new Vue();

export default {
  name: "Popup",
  computed: {
    ContextIsValid() {
      return this.context;
    },
    FileIsValid() {
      return this.file;
    },
  },
  data: () => ({
    tabs: null,
    text: "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.",
    context: "",
    contexts: [],
    file: null,
    files: [],
    snackbar: false,
    rules: [
      (value) =>
        !value ||
        value.size < 10000000 ||
        "File size should be less than 10 MB!",
    ],
  }),
  methods: {
    resetForm() {
      this.form = Object.assign({}, this.defaultForm);
      this.$refs.form.reset();
    },
    submit() {
      this.snackbar = true;
      this.resetForm();
    },
    uploadFile(file) {
      this.files.push(file);

      if (file.type.startsWith("image/")) {
        const img_src = window.URL.createObjectURL(file);
        this.$emit("uploadImage", img_src);
      }

      eventBus.$emit("file", file);
    },
    uploadText(context) {
      this.contexts.push(context);
      eventBus.$emit("context", context);
    },
  },
};
</script>