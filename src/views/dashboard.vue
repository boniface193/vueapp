<template>
  <section>
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

      <v-navigation-drawer
        v-model="drawer"
        :color="color"
        :expand-on-hover="expandOnHover"
        :src="bg"
        absolute
      >
        <v-list dense nav class="pt-12">
          <v-list-item
            class="my-12"
            v-for="item in items"
            :key="item.title"
            link
            router
            :to="item.route"
          >
            <v-list-item-icon>
              <v-icon>{{ item.icon }}</v-icon>
            </v-list-item-icon>

            <v-list-item-content>
              <v-list-item-title>{{ item.title }}</v-list-item-title>
            </v-list-item-content>
          </v-list-item>
        </v-list>
      </v-navigation-drawer>

      <v-container fluid class="background" style="padding-top: 10%">
        <v-container>
          <v-row>
            <v-col md="4">
              <v-subheader class="subtitle-1 txt-color">Employees</v-subheader>
            </v-col>

            <v-col md="4" class="offset-md-4 float-right">
              <v-btn dark class="txt-success txt-format form-control" depressed>Add New</v-btn>
            </v-col>
          </v-row>

          <v-app-bar flat rounded :color="color">
            <v-subheader class="txt-large txt-color">Josh Bakery Ventures</v-subheader>
            <v-spacer></v-spacer>
            <v-subheader class="txt-color">62, Bode Thomas, Surulere, Lagos</v-subheader>
          </v-app-bar>

          <section class="my-12">
            <v-card class="main-body" flat>
              <v-card-title>
                <v-row>
                  <v-col lg="2" md="12">
                    <v-select placeholder="Change" type="select"></v-select>
                  </v-col>
                  <v-col lg="2" md="12">
                    <v-btn depressed dark class="txt-success txt-format">change</v-btn>
                  </v-col>
                  <v-col lg="2" md="12">
                    <v-text-field
                      v-model="search"
                      append-icon="mdi-magnify"
                      label="Search"
                      single-line
                      hide-details
                    ></v-text-field>
                  </v-col>
                  <v-col sm="12"></v-col>
                </v-row>
              </v-card-title>
              <v-data-table
                :items-per-page="5"
                show-select
                loading="true"
                elevation-12
                :headers="headers"
                :items="desserts"
                class="elevation-1 mt-12"
              ></v-data-table>
            </v-card>
          </section>
        </v-container>
      </v-container>
    </v-app>
  </section>
</template>

<script>
export default {
  data() {
    return {
      drawer: true,
      color: "#fff",
      items: [
        { title: "Dashboard", icon: "mdi-view-grid-outline", route: "/login" },
        { title: "Photos", icon: "mdi-account-multiple-outline", route: "/" },
        { title: "About", icon: "mdi-dock-top", route: "/application" },
      ],
      expandOnHover: true,

      headers: [
        {
          text: "Dessert (100g serving)",
          align: "start",
          sortable: false,
          value: "name",
        },
        { text: "Calories", value: "calories" },
        { text: "Fat (g)", value: "fat" },
        { text: "Carbs (g)", value: "carbs" },
        { text: "Protein (g)", value: "protein" },
        { text: "Iron (%)", value: "iron" },
      ],
      desserts: [
        {
          name: "Frozen Yogurt",
          calories: 159,
          fat: 6.0,
          carbs: 24,
          protein: 4.0,
          iron: "1%",
        },
        {
          name: "Ice cream sandwich",
          calories: 237,
          fat: 9.0,
          carbs: 37,
          protein: 4.3,
          iron: "1%",
        },
      ],
    };
  },
};
</script>

<style lang="css" scoped>
.bg {
  background: #ffffff;
}
.text-color {
  color: #013c61;
}
.main-body {
  background: #e5e5e5;
}
table thead tr {
  border: green;
}

@media screen and (max-width: 960px) {
  .v-subheader.txt-color.theme--light {
    font-size: 12px;
    font-weight: 400;
  }

  .v-subheader.txt-large.txt-color.theme--light {
    font-size: 12px !important;
    display: flex;
    font-weight: 600;
    min-width: 50%;
  }

  .col-md-12.col-lg-2.col {
    min-width: 100%;
}

}
</style>