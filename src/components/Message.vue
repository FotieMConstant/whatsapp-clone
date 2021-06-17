<template>
  <div>
    <v-row v-if="me" class="d-flex justify-end">
      <div class="message sent pa-2 mr-4">
        <div class="mr-5">{{message}}</div>
        <div class="d-flex justify-end">
          <span class="text--disabled caption ml-3">{{timeStamp}}</span>
          <v-icon small class="ml-1" color="primary">mdi-check-all</v-icon>
        </div>
      </div>
    </v-row>
    <v-row v-else>
      <div class="message received pa-2 ml-4">
        <div class="mr-5">{{message}}</div>
        <div class="d-flex justify-end">
          <span class="text--disabled caption ml-3">{{timeStamp}}</span>
          <v-icon small class="ml-1">mdi-check-all</v-icon>
        </div>
      </div>
    </v-row>
  </div>
</template>
<script>
export default {
  props: {
    me: Boolean,
    message: String,
    timeStamp: String,
  },
};
</script>
<style>
/* making the first chat messagemargin */
.message:first-child {
  margin: 20px 0 8px;
}
.message.sent {
  background: #e1ffc7;
  border-radius: 10px 0px 10px 10px;
}
.message.received {
  background: #ffffff;
  border-radius: 0px 10px 10px 10px;
}
</style>