<template>
  <v-container dense>
    <v-row class="mt-12">
      <v-checkbox
        v-model="ex4"
        label="Context 1"
        color="amber accent-2"
        value="primary"
        hide-details
      >
      </v-checkbox>
      <v-checkbox
        v-model="ex4"
        label="Context 2"
        color="amber accent-2"
        value="secondary"
        hide-details
      >
      </v-checkbox>
      <v-checkbox
        v-model="ex4"
        label="Context 3"
        color="amber accent-2"
        value="success"
        hide-details
      >
      </v-checkbox>
      <v-checkbox
        v-model="ex4"
        label="Context 4"
        color="amber accent-2"
        value="info"
        hide-details
      >
      </v-checkbox>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: "ContextSelector",
  data: () => ({
    ex4: ["primary", "secondary", "success"],
  }),
};
</script>