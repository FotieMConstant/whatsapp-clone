<template>
  <span>
    <v-row no-gutters>
      <v-col cols="12" md="4">
        <v-card outlined tile>
          <!-- top left bar -->
          <TopLeftBar />
          <Search />
          <div class="__sideChatList">
            <span v-for="chat in chatsList" :key="chat.id" class="__chatItem">
              <ChatItem :chat="chat" />
            </span>
          </div>
        </v-card>
      </v-col>
      <v-col cols="12" sm="6" md="8">
        <v-card elevation="0">
          <Inbox />
        </v-card>
      </v-col>
    </v-row>
  </span>
</template>

<script>
import TopLeftBar from "../components/TopLeftBar";
import ChatItem from "../components/ChatItem";
import Search from "../components/Search";
import Inbox from "../components/Inbox";

export default {
  name: "Home",

  components: {
    TopLeftBar,
    ChatItem,
    Search,
    Inbox,
  },
  data() {
    return {
      chatsList: [
        {
          id: 0,
          name: "fotiecodes",
          lastMessage: "Yooo gee",
          lastTextTime: "Yesterday",
          totalMessagesInChat: 7,
          blueCheck: true,
          displayPicture:
            "https://avatars.githubusercontent.com/u/42372656?v=4",
        },
        {
          id: 1,
          name: "HSKK初级考试班级群",
          lastMessage: "同学们好！谁用微信？",
          lastTextTime: "15:30",
          totalMessagesInChat: 1,
          blueCheck: true,
          displayPicture:
            "https://blog.keatschinese.com/wp-content/uploads/2020/12/learning-the-chinese-language.jpg",
        },
        {
          id: 2,
          name: "yancodes",
          lastMessage: "The same guy I was with the last time I was there",
          lastTextTime: "07:15",
          totalMessagesInChat: 12,
          blueCheck: false,
          displayPicture:
            "https://pbs.twimg.com/profile_images/1172588555966844933/GD3slkzF_400x400.jpg",
        },
        {
          id: 3,
          name: "Longla",
          lastMessage: "Thanks bro",
          lastTextTime: "Yesterday",
          totalMessagesInChat: 1,
          blueCheck: false,
          displayPicture:
            "https://avatars.githubusercontent.com/u/44490676?v=4",
        },
        {
          id: 4,
          name: "fotiecodes",
          lastMessage: "Yooo gee",
          lastTextTime: "Yesterday",
          totalMessagesInChat: 15,
          blueCheck: false,
          displayPicture:
            "https://avatars.githubusercontent.com/u/42372656?v=4",
        },
        {
          id: 5,
          name: "fotiecodes",
          lastMessage: "Yooo gee",
          lastTextTime: "Yesterday",
          totalMessagesInChat: 1,
          blueCheck: true,
          displayPicture:
            "https://avatars.githubusercontent.com/u/42372656?v=4",
        },
        {
          id: 6,
          name: "fotiecodes",
          lastMessage: "Yooo gee",
          lastTextTime: "Yesterday",
          totalMessagesInChat: 10,
          blueCheck: false,
          displayPicture:
            "https://avatars.githubusercontent.com/u/42372656?v=4",
        },
        {
          id: 7,
          name: "fotiecodes",
          lastMessage: "Yooo gee",
          lastTextTime: "Yesterday",
          totalMessagesInChat: 3,
          blueCheck: false,
          displayPicture:
            "https://avatars.githubusercontent.com/u/42372656?v=4",
        },
      ],
    };
  },
};
</script>
<style scoped>
.__sideChatList {
  height: 500px;
  overflow-y: scroll;
}

.__sideChatList::-webkit-scrollbar {
  width: 6px;
  height: 6px !important;
}
/* Track */
/* .__sideChatList::-webkit-scrollbar-track {
  box-shadow: inset 0 0 3px grey;
} */
/* Handle */
.__sideChatList::-webkit-scrollbar-thumb {
  background: rgba(0, 0, 0, 0.2);
}
/* Handle on hover */
.__sideChatList::-webkit-scrollbar-thumb:hover {
  background: rgb(156, 156, 156);
}
.__chatItem {
  cursor: pointer;
}
</style>
