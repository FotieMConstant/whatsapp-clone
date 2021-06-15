<template>
  <span>
    <v-row no-gutters>
      <v-col cols="6" md="4">
        <v-card outlined tile>
          <!-- top left bar -->
          <TopLeftBar />
          <Search />
          <div class="__sideChatList">
            <ChatItem />
            <ChatItem />
            <ChatItem />
            <ChatItem />
            <ChatItem />
            <ChatItem />
            <ChatItem />
            <ChatItem />
          </div>
        </v-card>
      </v-col>
      <v-col cols="12" sm="6" md="8">
        <v-card class="pa-2" outlined tile>This is where the text will be place</v-card>
      </v-col>
    </v-row>
  </span>
</template>

<script>
import TopLeftBar from "../components/TopLeftBar";
import ChatItem from "../components/ChatItem";
import Search from "../components/Search";

export default {
  name: "Home",

  components: {
    TopLeftBar,
    ChatItem,
    Search,
  },
};
</script>
<style scoped>
.__sideChatList {
  height: 500px;
  overflow-y: scroll;
}
</style>
