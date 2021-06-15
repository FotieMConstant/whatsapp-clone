<template>
  <div>
    <v-app-bar elevation="0" class="pa-2 __statusBar" height="auto" dense>
      <div>
        <v-avatar size="40">
          <img src="https://avatars.githubusercontent.com/u/42372656?v=4" alt="fotiecodes" />
        </v-avatar>
        <span class="ml-3 mt-n2">fotiecodes</span>
        <div class="text--disabled caption ml-13 mt-n3">last seen today at 20:48</div>
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
          <v-list-item @click="() => {}">
            <v-list-item-title>Delete chat</v-list-item-title>
          </v-list-item>
        </v-list>
      </v-menu>
    </v-app-bar>
    <!-- chat area -->
    <div class="__theChat __areaPortrait" @contextmenu="show"></div>
    <!-- end chat area -->
    <!-- chat input field -->
    <v-container class="grey lighten-5 __chatInput">
      <v-row class="mt-1 ml-1 mr-1">
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
        <v-text-field
          class="__messageBox"
          flat
          label="Search or start new chat"
          rounded
          solo
          prepend-inner-icon="mdi-magnify"
        ></v-text-field>
      </v-row>
    </v-container>
    <!-- end chat input field -->
    <!-- right click on text area-->
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
        <v-list-item @click="() => {}">
          <v-list-item-title>Delete chat</v-list-item-title>
        </v-list-item>
      </v-list>
    </v-menu>
    <!-- end right click on text area -->
  </div>
</template>
<script>
export default {
  props: {
    chat: Object,
  },
  data() {
    return {
      showMenu: false,
      x: 0,
      y: 0,
      items: [
        { title: "Click Me" },
        { title: "Click Me" },
        { title: "Click Me" },
        { title: "Click Me 2" },
      ],
    };
  },
  methods: {
    show(e) {
      e.preventDefault();
      this.showMenu = false;
      this.x = e.clientX;
      this.y = e.clientY;
      this.$nextTick(() => {
        this.showMenu = true;
      });
    },
  },
};
</script>

<style>
.__statusBar {
  cursor: pointer;
}
.__theChat {
  height: 550px;
  width: 100%;
  background-image: url("https://whatsapp-73989.web.app/static/media/bg.2d472127.png");
  background-repeat: no-repeat;
  background-size: cover;
}
.__areaPortrait.div {
  margin: 0 auto;
  max-width: 600px;
  width: 100%;
}
.__chatInput {
  margin-top: -40px;
}
.__messageBox {
  width: 50%;
}
</style>