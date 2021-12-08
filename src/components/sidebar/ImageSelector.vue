<template>
      <v-container dense>
        <v-radio-group v-model="radioGroup">
          <v-radio
            v-for="n in 3"
            :key="n"
            :label="`Image ${n}`"
            :value="n"
            color="amber accent-2"
          ></v-radio>
        </v-radio-group>
      </v-container>
</template>

<script>
export default {
    name: 'ImageSelector',
    data: () => ({
      radioGroup: 1,
    }),
}
</script>