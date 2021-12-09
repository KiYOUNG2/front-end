<template>
  <v-container class="fill-height">
    <v-row class="fill-height pb-14" align="end">
      <v-col>
        <div
          v-for="(item, index) in chat"
          :key="index"
          :class="[
            'd-flex flex-row align-center my-2',
            item.from == 'user' ? 'justify-end' : null,
          ]"
        >
          <span v-if="item.from == 'user' && item.msg != null" class="blue--text mr-3" style="max-width: 60%; text-align: right;">{{
            item.msg
          }}</span>
          <v-avatar
            :color="item.from == 'user' ? 'grey' : 'amber accent-2'"
            size="36"
          >
            <span class="white--text">{{ item.from[0] }}</span>
          </v-avatar>
          <span v-if="item.from != 'user' && item.msg != null" class="blue--text ml-3" style="max-width: 60%; text-align: left;">{{
            item.msg
          }}</span>
        </div>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: "Message",
  props: ["chat"],
};
</script>