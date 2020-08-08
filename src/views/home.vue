<template>
  <v-container fluid class="background">
    <div>
      <v-container>
        <v-app-bar flat :color="color">
          <v-subheader class="subtitle-1 txt-color">Employees</v-subheader>
          <v-spacer></v-spacer>
          <v-btn dark class="txt-success txt-format">Add New</v-btn>
        </v-app-bar>

        <v-app-bar flat rounded>
          <v-subheader class="txt-large txt-color">Josh Bakery Ventures</v-subheader>
          <v-spacer></v-spacer>
           <v-subheader class="txt-color">62, Bode Thomas, Surulere, Lagos</v-subheader>
        </v-app-bar>
      </v-container>
    </div>
  </v-container>
</template>

<script>
export default {
  name: "home",

  data: () => ({
    color: "#e5e5e5",
  }),
};
</script>

<style>
.background {
  min-height: 100%;
  background: #e5e5e5;
}
.v-subheader.subtitle-1 {
  font-family: Roboto;
  font-style: normal;
  font-weight: 500;
  font-size: 26px;
  line-height: 15px;
}

.txt-color {
  color: #013c61 !important;
  letter-spacing: -0.65px;
}
.txt-success {
  background: #2bda53 !important;
  box-shadow: 0px 7px 15px rgba(43, 218, 83, 0.2);
  border-radius: 3px;
}

.txt-format {
  font-family: Roboto !important;
  font-style: normal;
  font-weight: 500;
  font-size: 8%;
  line-height: 22px;
}

.txt-large{
  font-family: Roboto !important;
  font-style: normal;
  font-weight: 500;
  font-size: 25px !important;
  line-height: 15px !important;
}
</style>