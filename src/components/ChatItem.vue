<template>
  <v-container>
    <v-row>
      <v-col cols="2" md="2">
        <v-avatar size="55">
          <img src="https://avatars.githubusercontent.com/u/42372656?v=4" alt="fotiecodes" />
        </v-avatar>
      </v-col>
      <v-col cols="12" sm="6" md="8">
        <div class="mt-1">
          <p>fotiecodes</p>
          <div class="text--disabled mt-n3 caption">
            <v-icon small class="mr-1">mdi-check-all</v-icon>You might want to check it out
          </div>
        </div>
      </v-col>
      <v-col class="caption" sm="2" md="2">
        <div class="mt-1 d-flex justify-end">07:27</div>
        <div class="d-flex justify-end">
          <v-badge color="green" content="7" class="mt-2" inline></v-badge>
        </div>
      </v-col>
    </v-row>
    <v-divider class="mt-4" inset></v-divider>
  </v-container>
</template>