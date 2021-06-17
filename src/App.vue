<template>
  <v-app>
    <v-main>
      <router-view />
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: "App",

  data() {
    //
    return {};
  },
};
</script>

<style>
/* hide scroll bar but keep functionality */
body::-webkit-scrollbar {
  display: none;
}
</style>