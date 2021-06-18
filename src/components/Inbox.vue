<template>
  <div>
    <v-app-bar elevation="0" class="pa-2 __statusBar" height="auto" dense>
      <div>
        <v-avatar size="40">
          <img :src="chat.displayPicture" :alt="chat.name" />
        </v-avatar>
        <span class="ml-3 mt-n2">{{chat.name}}</span>
        <div v-if="chat.lastSeen=== 'online'" class="text--disabled caption ml-13 mt-n3">Online</div>
        <div v-else class="text--disabled caption ml-13 mt-n3">last seen today at {{chat.lastSeen}}</div>
      </div>

      <v-spacer></v-spacer>

      <v-btn icon>
        <v-icon>mdi-magnify</v-icon>
      </v-btn>

      <v-menu
        left
        bottom
        offset-y
        allow-overflow
        nudge-right
        transition="scale-transition"
        origin="top right 0"
        class="pr-10"
        min-width="100"
      >
        <template v-slot:activator="{ on, attrs }">
          <v-btn icon v-bind="attrs" v-on="on">
            <v-icon>mdi-dots-vertical</v-icon>
          </v-btn>
        </template>

        <v-list>
          <v-list-item @click="() => {}">
            <v-list-item-title>Contact info</v-list-item-title>
          </v-list-item>
          <v-list-item @click="() => {}">
            <v-list-item-title>Select messages</v-list-item-title>
          </v-list-item>
          <v-list-item @click="() => {}">
            <v-list-item-title>Mute notifications</v-list-item-title>
          </v-list-item>
          <v-list-item @click="() => {}">
            <v-list-item-title>Clear messages</v-list-item-title>
          </v-list-item>
          <v-list-item @click="deleteChat">
            <v-list-item-title>Delete chat</v-list-item-title>
          </v-list-item>
        </v-list>
      </v-menu>
    </v-app-bar>
    <!-- chat area -->
    <div ref="messagesContainer" class="conversation-container __areaPortrait" @contextmenu="show">
      <span v-for="(chatMessage, index) in chat.messages" :class="`index-${index}`" :key="index">
        <!-- checking to make sure the received or sent actually contain data -->
        <Message
          v-if="chatMessage.received"
          :message="chatMessage.received"
          :timeStamp="chatMessage.timeStampReceived"
        />
        <Message
          v-if="chatMessage.sent"
          :message="chatMessage.sent"
          :timeStamp="chatMessage.timeStampSent"
          me
        />
      </span>
    </div>
    <!-- end chat area -->
    <!-- chat input field -->
    <v-container class="grey lighten-5 __chatInput">
      <v-row class="mt-0 ml-1 mb-n3">
        <span class="mt-1">
          <v-btn icon>
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="24" height="24">
              <path
                fill="currentColor"
                d="M9.153 11.603c.795 0 1.439-.879 1.439-1.962s-.644-1.962-1.439-1.962-1.439.879-1.439 1.962.644 1.962 1.439 1.962zm-3.204 1.362c-.026-.307-.131 5.218 6.063 5.551 6.066-.25 6.066-5.551 6.066-5.551-6.078 1.416-12.129 0-12.129 0zm11.363 1.108s-.669 1.959-5.051 1.959c-3.505 0-5.388-1.164-5.607-1.959 0 0 5.912 1.055 10.658 0zM11.804 1.011C5.609 1.011.978 6.033.978 12.228s4.826 10.761 11.021 10.761S23.02 18.423 23.02 12.228c.001-6.195-5.021-11.217-11.216-11.217zM12 21.354c-5.273 0-9.381-3.886-9.381-9.159s3.942-9.548 9.215-9.548 9.548 4.275 9.548 9.548c-.001 5.272-4.109 9.159-9.382 9.159zm3.108-9.751c.795 0 1.439-.879 1.439-1.962s-.644-1.962-1.439-1.962-1.439.879-1.439 1.962.644 1.962 1.439 1.962z"
              />
            </svg>
          </v-btn>
          <v-btn icon>
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="24" height="24">
              <path
                fill="currentColor"
                d="M1.816 15.556v.002c0 1.502.584 2.912 1.646 3.972s2.472 1.647 3.974 1.647a5.58 5.58 0 0 0 3.972-1.645l9.547-9.548c.769-.768 1.147-1.767 1.058-2.817-.079-.968-.548-1.927-1.319-2.698-1.594-1.592-4.068-1.711-5.517-.262l-7.916 7.915c-.881.881-.792 2.25.214 3.261.959.958 2.423 1.053 3.263.215l5.511-5.512c.28-.28.267-.722.053-.936l-.244-.244c-.191-.191-.567-.349-.957.04l-5.506 5.506c-.18.18-.635.127-.976-.214-.098-.097-.576-.613-.213-.973l7.915-7.917c.818-.817 2.267-.699 3.23.262.5.501.802 1.1.849 1.685.051.573-.156 1.111-.589 1.543l-9.547 9.549a3.97 3.97 0 0 1-2.829 1.171 3.975 3.975 0 0 1-2.83-1.173 3.973 3.973 0 0 1-1.172-2.828c0-1.071.415-2.076 1.172-2.83l7.209-7.211c.157-.157.264-.579.028-.814L11.5 4.36a.572.572 0 0 0-.834.018l-7.205 7.207a5.577 5.577 0 0 0-1.645 3.971z"
              />
            </svg>
          </v-btn>
        </span>
        <v-form @submit="sendMessage" id="__sendMessageForm">
          <v-text-field v-model="messageBody" flat placeholder="Type a message" rounded solo dense></v-text-field>
        </v-form>
        <v-btn icon class="ml-2 mt-1">
          <v-icon>mdi-microphone</v-icon>
        </v-btn>
      </v-row>
    </v-container>
    <!-- end chat input field -->
    <!-- right click on chat area-->
    <v-menu
      v-model="showMenu"
      :position-x="x"
      :position-y="y"
      absolute
      offset-y
      nudge-right
      transition="scale-transition"
      origin="top left 0"
    >
      <v-list>
        <v-list-item @click="() => {}">
          <v-list-item-title>Contact info</v-list-item-title>
        </v-list-item>
        <v-list-item @click="() => {}">
          <v-list-item-title>Select messages</v-list-item-title>
        </v-list-item>
        <v-list-item @click="() => {}">
          <v-list-item-title>Mute notifications</v-list-item-title>
        </v-list-item>
        <v-list-item @click="() => {}">
          <v-list-item-title>Clear messages</v-list-item-title>
        </v-list-item>
        <v-list-item @click="deleteChat">
          <v-list-item-title>Delete chat</v-list-item-title>
        </v-list-item>
      </v-list>
    </v-menu>
    <!-- end right click on chat area -->
  </div>
</template>
<script>
import Message from "../components/Message";
export default {
  components: {
    Message,
  },
  props: {
    chat: Object,
    chatsList: Array,
  },
  data() {
    return {
      messageBody: "", // message the user types to send in chat
      showMenu: false,
      x: 0,
      y: 0,
    };
  },
  methods: {
    // function to show the menu when the user right clicks
    show(e) {
      e.preventDefault();
      this.showMenu = false;
      this.x = e.clientX;
      this.y = e.clientY;
      this.$nextTick(() => {
        this.showMenu = true;
      });
    },
    // function to send message
    sendMessage(event) {
      event.preventDefault();
      console.log("sending message => " + this.messageBody);

      // get the current time we will use in sending the message
      const time = new Date();

      let hh = time.getHours();
      let mm = time.getMinutes();
      let timeStamp = hh + ":" + mm;
      // pushing the messaged entered to the chat.messages array of the chat object
      this.chat.messages.push({
        received: null,
        sent: this.messageBody,
        timeStampSent: timeStamp, // current time included in sent message
        timeStampReceived: null,
      });
      console.log(this.chat);
      this.chat.lastMessage = this.messageBody; // updating the last message on the chats list with the last message sent
      this.chat.lastTextTime = timeStamp; // updating the lastTextTime in chatList
      this.messageBody = ""; // setting the vatiable back to empty string when done
    },
    // function to scroll to the buttom automatically
    scrollToElement() {
      var content = this.$refs.messagesContainer; // get the container to be scrolled in
      content.scrollTop = content.scrollHeight; // making the scrollHeight the scroll top
      console.log(
        "scroll height is " +
          content.scrollHeight +
          " scroll Top is " +
          content.scrollTop
      );
    },
    deleteChat() {
      console.log("deleteChat");
      this.chatsList.map((item, index) => {
        if (item.id == this.chat.id) {
          this.chatsList.splice(index, 1);
        }
      });
    },
  },
  // update hook
  // read this better understant https://v3.vuejs.org/api/options-lifecycle-hooks.html#updated

  updated() {
    // using $nextTick makes Code that will run only after the
    // entire view has been re-rendered
    this.$nextTick(() => this.scrollToElement());
  },
};
</script>

<style>
.__statusBar {
  cursor: pointer;
}
.conversation-container {
  height: 518px;
  width: 100%;
  background-image: url("https://whatsapp-73989.web.app/static/media/bg.2d472127.png");
  background-repeat: no-repeat;
  background-size: cover;
  overflow-y: scroll;
  overflow-x: hidden; /* to make it scrollable */
}
.conversation-container::-webkit-scrollbar {
  width: 6px;
  height: 6px !important;
}
/* Handle */
.conversation-container::-webkit-scrollbar-thumb {
  background: rgba(0, 0, 0, 0.2);
}
.__areaPortrait.div {
  margin: 0 auto;
  max-width: 600px;
  width: 100%;
}
.__chatInput {
  position: fixed;
  bottom: -16px;
}

#__sendMessageForm {
  width: 66%;
}
</style>