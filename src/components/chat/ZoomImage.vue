<template>
  <v-dialog v-model="dialog" max-width="50%">
    <template v-slot:activator="{ on, attrs }">
      <v-img
        style="max-width: 35%; margin-left: 1%; margin-right: 1%"
        :src="item.img"
        v-bind="attrs"
        v-on="on"
      >
      </v-img>
    </template>
    <v-card>
      <v-img :src="item.img" @click="dialog = false"></v-img>
    </v-card>
  </v-dialog>
</template>

<script>
export default {
  name: "ZoomImage",
  props: ["item"],
  data: () => ({
    dialog: false,
  }),
};
</script>