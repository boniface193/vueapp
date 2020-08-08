<template>
  <v-app>
    <v-app-bar app hidden-lg-only flat :color="color">
      <div class="d-flex align-center">
        <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          src="../assets/logo.png"
          transition="scale-transition"
          width="40"
        />

        <nav class="text-color">
          <span class="title">Get</span>Change
        </nav>
      </div>

      <v-spacer></v-spacer>

      <v-avatar color="grey" size="36">
        <v-img src></v-img>
      </v-avatar>
      <h5 class="ml-2">Hi, John</h5>

      <v-menu>
        <template v-slot:activator="{on, attrs}">
          <v-btn small v-on="on" v-bind="attrs" class="ml-2" depressed>
            <v-icon>mdi-menu-down</v-icon>
          </v-btn>
        </template>
        <v-list>
          <v-list-item v-for="(item, index) in items" :key="index">
            <v-list-item-title>{{item.title}}</v-list-item-title>
          </v-list-item>
        </v-list>
      </v-menu>
    </v-app-bar>
  </v-app>
</template>

<script>
export default {
  data: () => ({
    color: "#fff",
    items: [
      { title: "Click Me" },
      { title: "Click Me" },
      { title: "Click Me" },
      { title: "Click Me 2" },
    ],
  }),
};
</script>

<style lang="css" scoped>
.bg {
  background: #ffffff;
}
.text-color {
  color: #013c61;
}
</style>