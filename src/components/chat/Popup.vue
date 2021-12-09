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
        <v-toolbar color="amber accent-2" dark flat>
          <v-toolbar-title>Upload files</v-toolbar-title>
          <template v-slot:extension>
            <v-tabs v-model="tabs" centered>
              <v-tabs-slider color="yellow"></v-tabs-slider>
              <v-tab>Context</v-tab>
              <v-tab>Image</v-tab>
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
                        v-model="form.context"
                        color="teal"
                        maxlength="1000"
                      >
                        <template v-slot:label>
                          <div>Context</div>
                        </template>
                      </v-textarea>
                    </v-col>
                  </v-row>
                </v-container>
                <v-card-actions>
                  <v-btn text @click="dialog.value = false">Close </v-btn>
                  <v-spacer></v-spacer>
                  <v-btn
                    :disabled="!formIsValid"
                    text
                    color="primary"
                    type="submit"
                    @click="uploadText(form.context)"
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
                        v-model="files"
                        :rules="rules"
                        accept="image/png, image/jpeg, image/bmp"
                        placeholder="Pick an image"
                        prepend-icon="mdi-camera"
                        label="Image"
                      >
                      </v-file-input>
                    </v-col>
                  </v-row>
                </v-container>
                <v-card-actions>
                  <v-btn text @click="dialog.value = false">Close </v-btn>
                  <v-spacer></v-spacer>
                  <v-btn text color="primary" type="submit" @click="uploadFile">
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
import axios from "axios";

const defaultForm = Object.freeze({
  context: "",
});

export default {
  name: "Popup",
  computed: {
    formIsValid() {
      return this.form.context;
    },
  },
  data: () => ({
    tabs: null,
    text: "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.",
    form: Object.assign({}, defaultForm),
    snackbar: false,
    defaultForm,
    rules: [
      (value) =>
        !value ||
        value.size < 10000000 ||
        "Image size should be less than 10 MB!",
    ],
    files: [],
    contexts: [],
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
    selectFile(file) {
      this.progress = 0;
      this.currentFile = file;
    },
    uploadText(context) {
      this.contexts.push(context);
      console.log(this.contexts);
    },
    async uploadFile() {
      var fd = new FormData();
      fd.append("files", this.files);

      if (this.files.type.startsWith('image/')){
        const img_src = window.URL.createObjectURL(this.files);
        this.$emit('uploadImage', img_src)
      }

      await axios
        .post("http://127.0.0.1:5000/upload", fd, {
          headers: {
            "Content-Type": "multipart/form-data",
          },
        })
        .then((response) => {
          console.log("SUCCESS!!");
          console.log(response.data);
        })
        .catch(function () {
          console.log("FAILURE!!");
        });
    },
  },
};
</script>