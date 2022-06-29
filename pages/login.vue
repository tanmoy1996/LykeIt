<template>
  <v-card tile flat 
  height="100vh" 
  class="d-flex justify-center align-center">
    <v-row class="no-gutters fill-height">
      <v-col cols md="6" class="d-flex align-center">
          <nuxt-img
          width="700"
          class="rot-20"
          src="/login-img.jpg" alt="Login Pic"/>
        </v-col>
        <v-col cols md="6">
          <v-card flat class="pa-12">
            <v-card-text class="pb-0">
              <h1 class="text-work-san f-32">welcome back</h1>
              <p class="mt-3 f-20">Lorem ipsum dolor sit, amet consectetur adipisicing elit. Iusto, quae. Voluptas, vitae eligendi</p>
            </v-card-text>
            <v-card-text>
              <Button width="500" height="50">
                <v-text-field
                  solo
                  flat
                  dense
                  hide-details
                  color="black"
                  label="User Name / Email"
                  prepend-inner-icon="mdi-account"
                  />
              </Button>
              <Button width="500" height="50" class="mt-5">
                <v-text-field
                  solo
                  flat
                  dense
                  hide-details
                  color="black"
                  prepend-inner-icon="mdi-lock"
                  :append-icon="visible ? 'mdi-eye' : 'mdi-eye-off'"
                  :type="visible ? 'text' : 'password'"
                  @click:append="() => (visible = !visible)"
                  label="Password"
                  />
              </Button>
            </v-card-text>
            <v-btn text small class="my-2"
              >Forgot Password</v-btn>
            <v-card-actions>
              <Button width="100">
                <p class="mb-0">Login</p>
              </Button>
              <Button width="200">
                <p class="mb-0">Create Account</p>
              </Button>
            </v-card-actions>
          </v-card>
        </v-col>
        
      </v-row>
  </v-card>
      
</template>

<script>
import Button from '~/components/Button.vue'
export default {
    layout: "LoginLayout",
    data() {
        return {
            visible: false,
            login: {
                username: "",
                password: ""
            }
        };
    },
    components: { Button }
}
</script>

<style scoped>
.welcome{
  letter-spacing: 0px;
  font-family: 'Berkshire Swash', cursive;
  font-size:3.5vw;
  margin: 12px 0;
}
.welcome--desc{
  color:rgb(172, 172, 172);
  font-family:Verdana, Geneva, Tahoma, sans-serif;
}
.decoration{
  width:20px;
  height:32px;
  margin-right:5px;
}
.card{
  height:80vh;
  width:65vw;
}
@media screen and (max-width: 959px) {
  .welcome{
    font-size:5vw;
  }
  .card{
    height:90vh;
    width:70vw;
  }
}
</style>

<!-- <v-flex xs12 sm10 offset-sm1 md="8" offset-md="2">
        <v-card elevation="7" class="secondarygrad rounded-lg">
          <v-row style="margin: 0px">
            <v-flex xs12 sm5 md5>
              <v-card
                color="transparent"
                flat
                style="padding: 10px; text-align: center !important"
              >
                <v-card-text style="margin-bottom: 25px">
                  <img
                    :src="logo"
                    alt="Godial Logo"
                    style="
                      width: 80px;
                      height: auto;
                      border-radius: 50px;
                      margin-bottom: 10px;
                    "
                  />
                  <h2 style="margin-bottom: 30px">Godial Enterprise</h2>
                  <h3 style="margin: 5px 0px">Automatic Call Dialer and CRM</h3>
                  <div style="padding: 5px 15px; text-align: center">
                    <h5
                      style="
                        line-height: 17px;
                        font-weight: 500;
                        font-size: 12px;
                      "
                    >
                      Setup your call center in minutes. Simply create your
                      account, add team, download team app and start calling.
                    </h5>
                  </div>
                </v-card-text>
                <v-footer color="transparent" absolute>
                  <v-flex style="text-align: center !important">
                    <p
                      style="font-size: 12px; opacity: 0.6; margin-bottom: 0px"
                    >
                      © 2020 Godial Enterprise. All rights reserved
                    </p>
                  </v-flex>
                </v-footer>
              </v-card>
            </v-flex>
            <v-flex xs12 sm7 md7 style="padding: 0px; margin: 0px">
              <v-card
                v-if="loginDisplay"
                color="transparent"
                elevation="0"
                style="padding: 15px 50px; text-align: center"
                @keyup.enter="doLogin"
              >
                <v-card-title primary-title class="justify-center"
                  >Welcome to GoDial</v-card-title
                >
                <v-card-subtitle>
                  Login to your GoDial account with your username and password
                </v-card-subtitle>

                <v-card-text>
                  <v-flex xs12 sm10 offset-sm1 md10 offset-md1>
                    <v-text-field
                      v-model="login.username"
                      dense
                      label="User Name / Email"
                      outlined
                      prepend-inner-icon="account_circle"
                    ></v-text-field>
                  </v-flex>
                  <v-flex xs12 sm10 offset-sm1 md10 offset-md1>
                    <v-text-field
                      v-model="login.password"
                      dense
                      label="Password"
                      outlined
                      :append-icon="visible ? 'visibility' : 'visibility_off'"
                      :type="visible ? 'text' : 'password'"
                      prepend-inner-icon="lock"
                      @click:append="() => (visible = !visible)"
                    ></v-text-field>
                  </v-flex>

                  <v-flex
                    xs12
                    sm10
                    offset-sm1
                    md10
                    offset-md1
                    style="text-align: center !important; margin-bottom: 10px"
                  >
                    <v-btn
                      text
                      color="secondary lighten-3"
                      style="font-size: 12px; text-transform: none"
                      small
                      @click="forgotPasswordDisplay = true"
                      >Forgot Password</v-btn
                    >
                  </v-flex>
                  <v-flex
                    xs12
                    sm10
                    offset-sm1
                    md10
                    offset-md1
                    style="margin-bottom: 10px"
                  >
                    <v-btn color="black white--text" block @click="doLogin"
                      >Login</v-btn
                    >
                  </v-flex>
                  <v-flex xs12 sm10 offset-sm1 md10 offset-md1>
                    <v-btn
                      color="black white--text"
                      block
                      @click="signupDialogFun()"
                      >Create Account</v-btn
                    >
                  </v-flex>
                </v-card-text>
              </v-card>
            </v-flex>
          </v-row>
        </v-card>
      </v-flex>
    </v-row>

    !-- forgot password dialog --
    <v-dialog v-model="forgotPasswordDisplay" width="400" persistent>
      <v-card class="mx-auto">
        <v-card-title class="primarygrad">
          <h4
            style="
              font-size: 18px;
              color: #fafafa;
              letter-spacing: 0.5px;
              font-weight: 500;
            "
          >
            Forgot Password
          </h4>
        </v-card-title>
        <v-divider></v-divider>
        <v-card-text style="padding: 20px">
          <v-text-field
            v-model="forgotItem.email"
            dense
            label="Email"
            prepend-inner-icon="email"
            outlined
          ></v-text-field>
        </v-card-text>
        <v-divider></v-divider>
        <v-card-actions>
          <v-btn text @click="forgotPasswordDisplay = false">Close</v-btn>
          <v-spacer></v-spacer>
          <v-btn color="primarygrad white--text" @click="forgotPassword"
            >Reset</v-btn
          >
        </v-card-actions>
      </v-card>
    </v-dialog>

    !-- loader --
    <v-dialog v-model="dialog" persistent width="300">
      <v-card color="primarygrad white--text" dark>
        <v-card-text>
          Please wait
          <v-progress-linear
            indeterminate
            color="white"
            class="mb-0"
          ></v-progress-linear>
        </v-card-text>
      </v-card>
    </v-dialog>

    !-- signup page --
    <v-dialog v-model="signupDialog" max-width="600" persistent>
      <v-card elevation="0">
        <v-card-title class="primary">
          <h3 style="color: #fafafa; font-size: 20px; font-weight: 500">
            Sign Up
          </h3>
          <v-spacer></v-spacer>
          <v-btn
            fab
            small
            text
            class="white--text"
            @click="signupDialog = false"
          >
            <v-icon :size="22">close</v-icon>
          </v-btn>
        </v-card-title>

        <v-card-text style="padding: 0px; margin: 0px">
          <v-stepper v-model="step" style="box-shadow: none">
            <v-stepper-header>
              <v-stepper-step :complete="step > 1" step="1"
                >Organization</v-stepper-step
              >
              <v-divider></v-divider>
              <v-stepper-step step="2">Account</v-stepper-step>
            </v-stepper-header>

            <v-stepper-items>
              <v-stepper-content step="1">
                <v-card color="transparent">
                  <v-card-text>
                    <v-flex xs12 sm10 offset-sm1 md10 offset-md1>
                      <v-text-field
                        v-model="signup.nameOfCompany"
                        dense
                        prepend-inner-icon="business"
                        label="Organization Name*"
                        outlined
                      ></v-text-field>
                    </v-flex>
                    <v-flex xs12 sm10 offset-sm1 md10 offset-md1>
                      <v-select
                        v-model="signup.size.value"
                        dense
                        prepend-inner-icon="supervised_user_circle"
                        label="Organization Size"
                        :items="[
                          { text: 'Small (<10 Members)', value: 10 },
                          { text: 'Medium (<100 Members)', value: 100 },
                          { text: 'Large (100+ Members)', value: 500 },
                        ]"
                        outlined
                      ></v-select>
                    </v-flex>

                    <v-flex xs12 sm10 offset-sm1 md10 offset-md1>
                      <v-autocomplete
                        v-model="signup.country"
                        :items="getCountriesList()"
                        label="Country"
                        prepend-inner-icon="location_on"
                        item-text="name"
                        item-value="name"
                        outlined
                        dense
                        required
                      ></v-autocomplete>
                    </v-flex>
                  </v-card-text>
                </v-card>
              </v-stepper-content>

              <v-stepper-content step="2">
                <v-card color="transparent">
                  <v-card-text>
                    <v-flex xs12 sm10 offset-sm1 md10 offset-md1>
                      <v-text-field
                        v-model="signup.nameOfUser"
                        dense
                        prepend-inner-icon="perm_contact_calendar"
                        label="Name *"
                        outlined
                      ></v-text-field>
                    </v-flex>

                    <v-flex
                      xs12
                      sm10
                      offset-sm1
                      md10
                      offset-md1
                      style="margin-bottom: 25px"
                    >
                      <vue-tel-input
                        v-model="signup.phone"
                        :valid-characters-only="true"
                        @input="getPhoneNumber"
                      ></vue-tel-input>
                    </v-flex>

                    <v-flex xs12 sm10 offset-sm1 md10 offset-md1>
                      <v-text-field
                        v-model="signup.email"
                        dense
                        :rules="rulesEmail"
                        prepend-inner-icon="email"
                        label="Email"
                        outlined
                      ></v-text-field>
                    </v-flex>
                    <v-flex xs12 sm10 offset-sm1 md10 offset-md1>
                      <v-text-field
                        :value="signup.userid.toLowerCase()"
                        dense
                        :rules="rulesUsername"
                        prepend-inner-icon="account_circle"
                        label="User Name *"
                        outlined
                        @input="signup.userid = $event.toLowerCase()"
                      ></v-text-field>
                    </v-flex>

                    <v-flex xs12 sm10 offset-sm1 md10 offset-md1>
                      <v-text-field
                        v-model="signup.password"
                        dense
                        prepend-inner-icon="lock"
                        label="Password *"
                        :append-icon="visible ? 'visibility' : 'visibility_off'"
                        :type="visible ? 'text' : 'password'"
                        outlined
                        :rules="passwordRules"
                        @click:append="() => (visible = !visible)"
                      ></v-text-field>
                    </v-flex>

                    <v-flex xs12 sm10 offset-sm1 md10 offset-md1>
                      <v-text-field
                        v-model="signup.confirmPwd"
                        dense
                        prepend-inner-icon="lock"
                        label="Confirm Password *"
                        :append-icon="
                          visibleConfirm ? 'visibility' : 'visibility_off'
                        "
                        :type="visibleConfirm ? 'text' : 'password'"
                        outlined
                        :rules="confirmPwdRules"
                        @click:append="() => (visibleConfirm = !visibleConfirm)"
                      ></v-text-field>
                    </v-flex>

                    <v-flex xs12 sm10 offset-sm1 md10 offset-md1>
                      <v-checkbox v-model="termsCheckbox" color="green">
                        <template v-slot:label>
                          <div>
                            I have read and agree to the
                            <v-tooltip bottom>
                              <template v-slot:activator="{ on }">
                                <a
                                  target="_blank"
                                  href="https://godial.cc/terms.html"
                                  @click.stop
                                  v-on="on"
                                >
                                  Terms and Conditions
                                </a>
                              </template>
                              Terms and Conditions
                            </v-tooltip>
                            and
                            <v-tooltip bottom>
                              <template v-slot:activator="{ on }">
                                <a
                                  target="_blank"
                                  href="https://godial.cc/privacy.html"
                                  @click.stop
                                  v-on="on"
                                >
                                  Privacy Policy
                                </a>
                              </template>
                              Privacy Policy
                            </v-tooltip>
                          </div>
                        </template>
                      </v-checkbox>
                    </v-flex>
                  </v-card-text>
                </v-card>
              </v-stepper-content>
            </v-stepper-items>
          </v-stepper>
        </v-card-text>

        <v-divider></v-divider>

        <v-card-actions>
          <v-btn v-if="step != 1" text @click="step--">Back</v-btn>
          <v-spacer></v-spacer>
          <v-btn v-if="step != 2" color="primary" @click="next">Next</v-btn>
          <v-btn
            v-else
            color="primary"
            :disabled="dialog ? true : false"
            :loading="dialog ? true : false"
            @click="doSignup"
            >Sign Up</v-btn
          >
        </v-card-actions>
      </v-card>
    </v-dialog> -->