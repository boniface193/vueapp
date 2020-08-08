<template>
  <div class="background">
    <v-app>
      <v-row>
        <v-col lg="5" class="py-0 hidden-md-and-down">
          <v-carousel height="100%" hide-delimiter-background show-arrows-on-hover>
            <v-carousel-item v-for="(slide, i) in slides" :key="i">
              <v-sheet height="100%">
                <v-row :color="colors[i]" class="fill-height" align-lg="center" justify="center">
                  <div class="heading-text">{{slide.heading}}</div>
                  <div class="mx-12 footer-text">{{ slide.title }} Slide</div>
                </v-row>
              </v-sheet>
            </v-carousel-item>
          </v-carousel>
        </v-col>
        <v-col lg="7" md="12">
          <v-container>
            <div>
              <v-alert  v-model="is_alertShow" type="error">{{errors}}</v-alert>
            </div>
            <div class="txt-center">
              <h4 class="form-text">Create your free account</h4>
              <p class="form-text-sm">
                Already registered?
                <span>Sign in</span>
              </p>
            </div>
            <v-card class="mx-auto card" flat elevation="15">
              <v-card-text>
                <v-form   method="post">
                  <v-container>
                    <v-row>
                      <v-col lg="6" cols="12">
                        <v-text-field
                          v-model="firstname"
                          :rules="nameRules"
                          :counter="15"
                          append-icon="mdi-account-outline"
                          label="First Name"
                          required
                        ></v-text-field>
                      </v-col>

                      <v-col lg="6" cols="12">
                        <v-text-field
                          v-model="lastname"
                          :rules="nameRules"
                          :counter="10"
                          append-icon="mdi-account-outline"
                          label="Last Name"
                          required
                        ></v-text-field>
                      </v-col>
                    </v-row>
                    <v-row>
                      <v-col lg="12" md="12">
                        <v-text-field
                          v-model="email"
                          append-icon="mdi-at"
                          :rules="emailRules"
                          label="Email"
                          required
                        ></v-text-field>
                      </v-col>
                    </v-row>
                    <v-row>
                      <v-col lg="12" md="12">
                        <v-text-field
                          v-model="password"
                          :append-icon="show1 ? 'mdi-eye' : 'mdi-eye-off'"
                          :rules="[rules.required, rules.min]"
                          :type="show1 ? 'text' : 'password'"
                          name="email"
                          label="Password"
                          hint="At least 8 characters"
                          required
                          counter
                          @click:append="show1 = !show1"
                        ></v-text-field>
                      </v-col>
                    </v-row>
                  </v-container>
                  <div class="d-flex flex-right">
                    <v-btn
                      dark
                      depressed
                      class="btn"
                      @click="loginUser"
                      :loading="loading"
                    >Continue</v-btn>
                  </div>
                </v-form>
              </v-card-text>
            </v-card>
          </v-container>
          <v-container fluid>
            <v-footer transparent>
              <p class="footer">
                By siging up, you agree to our
                <span class>Terms</span> and
                <span>Privacy Policy</span>
              </p>
              <v-spacer></v-spacer>
              <div>&copy; {{ new Date().getFullYear() }}</div>
            </v-footer>
          </v-container>
        </v-col>
      </v-row>
    </v-app>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "login",

  data() {
    return {
      errors: [],
      loading: false,
      // valid: false,
      is_alertShow: false,
      firstname: "",
      lastname: "",
      nameRules: [
        (v) => !!v || "Name is required",
        (v) => v.length <= 15 || "Name must be less than 15 characters",
      ],
      email: "",
      emailRules: [
        (v) => !!v || "E-mail is required",
        (v) => /.+@.+/.test(v) || "E-mail must be valid",
      ],
      password: "",
      show1: false,

      rules: {
        required: (value) => !!value || "Required.",
        min: (v) => v.length >= 8 || "Min 8 characters",
        emailMatch: () => "The email and password you entered don't match",
      },
      colors: [
          'indigo',
          'warning',
        ],
      slides: [
        {
          title:
            "Lorem ipsum dolor sit amet consectetur adipisicing elit. Nesciunt, quia!",
          heading: "No Hazzles",
          image: "https://cdn.vuetifyjs.com/images/carousel/squirrel.jpg",
        },
        {
          title:
            "Lorem ipsum dolor sit amet consectetur adipisicing elit. Nesciunt, quia!",
          heading: "No Hazzles",
        },
      ],
    };
  },

  //   API calls is here
  methods: {
    validEmail(email) {
      var re = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
      return re.test(email);
    },
    loginUser() {
      console.log(this.loginUser)
      this.errors = [];

      if (!this.validEmail(this.email)) {
        this.errors.push("Valid email required.");
      }
      this.loading = true;



      axios.post("https://jsonplaceholder.typicode.com/posts", {
        'name': this.firstname,
        'username': this.lastname,
        'address.city': this.email,
        'password': this.password
      })
        .then((response) => {
          console.log(response.data);
          
          this.redirectUser();
        })
        .catch((error) => {
          console.log(error);
          this.errors.push(error.message)
          this.is_alertShow = true
          this.loading =false
        });
    },

    redirectUser(){
      this.$router.push({name: 'dashboard'})
    }
  },
};
</script>

<style lang="css" scoped>
.background {
  background-color: #e5e5e5 !important;
}
.footer-bg {
  background-color: inherit;
}
.footer-text {
  font-family: Roboto;
  font-style: normal;
  font-weight: normal;
  height: 100%;
  font-size: 15px;
  line-height: 36px;
  text-align: center;
}

.heading-text {
  margin-top: 80%;
}

.form-text {
  font-family: Roboto;
  font-style: normal;
  font-weight: 500;
  font-size: 34px;
  line-height: 46px;
  letter-spacing: 0.4px;
  color: #013c61 !important;
  position: absolute;
  height: 46px;
  margin-top: 5%;
}

.form-text-sm {
  font-family: Roboto;
  font-style: normal;
  font-weight: normal;
  font-size: 18px;
  line-height: 18px;
  letter-spacing: -0.102857px;
  color: #013c61 !important;
  position: absolute;
  margin-top: 10%;
}

.form-text-sm span {
  color: #2bda53;
}

.btn {
  background-color: #2bda53 !important;
  float: right;
}

.card {
  margin-top: 30%;
  justify-content: center;
  box-shadow: 0px 20px 50px #eaeee9;
  border-radius: 5px;
}

.footer {
  font-family: Roboto;
  font-style: normal;
  font-weight: normal;
  font-size: 13px;
  line-height: 18px;
  letter-spacing: -0.05px;

  color: #6a7e8a;
}

.container.container--fluid footer {
  margin-top: 10%;
  background-color: #fff;
}

@media screen and (max-width: 960px) {
  .form-text {
    font-size: 20px;
    color: #013c61 !important;
  }
  .txt-center {
    display: flex;
    justify-content: center;
  }
  .form-text-sm {
    font-size: 12px;
    color: #013c61 !important;
    margin-top: 20%;
  }
  .btn {
    width: 100%;
  }
  .card{
    margin-top: 35%;
  }
}
</style>