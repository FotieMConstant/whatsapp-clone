<template>
  <v-container id="__chat">
    <v-row>
      <v-col cols="2" md="2">
        <v-avatar size="55">
          <img :src="chat.displayPicture" alt="fotiecodes" />
        </v-avatar>
      </v-col>
      <v-col cols="5" sm="6" md="8">
        <div class="mt-1">
          <p>{{chat.name}}</p>
          <div class="text--disabled mt-n3 caption">
            <v-icon v-if="chat.blueCheck" small class="mr-1" color="primary">mdi-check-all</v-icon>
            <v-icon v-else small class="mr-1">mdi-check-all</v-icon>
            <span v-html="truncate(chat.lastMessage)"></span>
          </div>
        </div>
      </v-col>
      <v-col class="caption" sm="2" md="2">
        <div class="mt-1 d-flex justify-end">{{chat.lastTextTime}}</div>
        <div class="d-flex justify-end">
          <v-badge color="green" :content="chat.totalMessagesInChat" class="mt-2" inline></v-badge>
        </div>
      </v-col>
    </v-row>
    <v-divider class="mt-4" inset></v-divider>
  </v-container>
</template>
<script>
export default {
  props: {
    chat: Object,
  },
  data() {
    return {};
  },
  methods: {
    // function to Truncate text to fit in 3 lines and show three dots in end In Html
    truncate(text, size = 40) {
      return text.length > size ? text.slice(0, size - 1) + "..." : text;
    },
  },
};
</script>

<style>
.__chat:hover {
  background-color: green;
}
</style>