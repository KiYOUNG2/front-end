<template>
  <v-container>
    <section style="height: 700px; overflow-y: auto; overflow-x: hidden">
      <v-row align="end" style="padding: 1%">
        <v-col>
          <div
            v-for="(item, index) in chat"
            :key="index"
            :class="[
              'd-flex flex-row align-center my-2',
              item.from == 'user' ? 'justify-end' : null,
            ]"
          >
            <span
              v-if="item.from == 'user' && item.msg != null"
              class="blue--text mr-3"
              style="max-width: 60%; text-align: right"
              >{{ item.msg }}</span
            >
            <ZoomImage
              v-if="item.from == 'user' && item.img != null"
              v-bind:item="item"
            />
            <v-avatar
              :color="item.from == 'user' ? 'grey' : 'amber accent-2'"
              size="36"
            >
              <span class="white--text">{{ item.from[0] }}</span>
            </v-avatar>
            <span
              v-if="item.from != 'user' && item.msg != null"
              class="blue--text ml-3"
              style="max-width: 60%; text-align: left"
              >{{ item.msg }}</span
            >
            <ZoomImage
              v-if="item.from != 'user' && item.img != null"
              v-bind:item="item"
            />
          </div>
        </v-col>
      </v-row>
    </section>
  </v-container>
</template>

<script>
import ZoomImage from "./ZoomImage.vue";

export default {
  name: "Message",
  components: {
    ZoomImage,
  },
  props: ["chat"],
};
</script>