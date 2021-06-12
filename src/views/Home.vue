<template>
  <span>
    <v-row no-gutters>
      <v-col cols="6" md="4">
        <v-card class="pa-0" outlined tile>
          <!-- top left bar -->
          <TopLeftBar />
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

export default {
  name: "Home",

  components: {
    TopLeftBar,
  },
};
</script>
