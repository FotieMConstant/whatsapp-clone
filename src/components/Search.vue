<template>
  <div>
    <v-container class="grey lighten-5">
      <v-form id="__searchFilterForm">
        <v-text-field
          v-model="searchTerm"
          class="mb-n5"
          flat
          placeholder="Search or start new chat"
          rounded
          solo
          dense
          prepend-inner-icon="mdi-magnify"
        ></v-text-field>
      </v-form>
    </v-container>
    <v-divider></v-divider>
  </div>
</template>
<script>
export default {
  data() {
    return {
      searchTerm: null,
    };
  },
  watch: {
    searchTerm: function (newSearchTerm, oldSearchTerm) {
      if (newSearchTerm)
        console.log("live filtering =>", newSearchTerm, oldSearchTerm);
      this.$emit("onFilterFromChild", newSearchTerm); //emiting to the parent which todo to be deleted
    },
  },
};
</script>
<style scoped>
#__searchFilterForm {
  width: 96%;
}
</style>