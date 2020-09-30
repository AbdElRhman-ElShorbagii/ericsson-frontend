<template>
  <v-app id="login">
    <v-main class="primary">
      <v-container class="fill-height" fluid>
        <v-row align="center" justify="center">
          <v-col cols="12" sm="8" md="4">
            <v-card class="rounded-lg elevation-1 pa-3">
              <v-card-text>
                <div class="layout column align-center">
                  <img
                    src="@/assets/images/logo.png"
                    alt="iSchool"
                    width="200"
                    height="101"
                  />
                  <h1 class="flex my-4 primary--text">iSchool Sales Panel</h1>
                </div>
                <v-form ref="form" v-model="valid" @submit.prevent="login">
                  <v-text-field
                    class="mb-3"
                    append-icon="mdi-account"
                    name="login"
                    label="Email"
                    v-model="email"
                    :rules="[rules.required, rules.email]"
                  />
                  <v-text-field
                    :type="hidePassword ? 'password' : 'text'"
                    :append-icon="
                      hidePassword ? 'visibility_off' : 'visibility'
                    "
                    name="password"
                    label="Password"
                    id="password"
                    :rules="[rules.required, rules.password]"
                    v-model="password"
                    @click:append="hidePassword = !hidePassword"
                  />
                  <v-spacer></v-spacer>
                  <v-btn block color="primary" :disabled="!valid" @click="login"
                    >Login</v-btn
                  >
                </v-form>
              </v-card-text>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
      <notifications group="auth" position="bottom right" />
      <v-overlay :value="overlay">
        <v-progress-circular indeterminate size="64"></v-progress-circular>
      </v-overlay>
    </v-main>
  </v-app>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      valid: true,
      overlay: false,
      email: '',
      password: '',
      errors: [],
      hidePassword: true,
      rules: {
        required: v => !!v || "Required.",
        email: v =>
          /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/.test(
            v
          ) || "Email must be valid",
        password: v =>
          v.length >= 6 || "Password must be grate than 6 characters"
      }
    };
  },
  watch: {
    overlay(val) {
      val &&
        setTimeout(() => {
          this.overlay = false;
        }, 3000);
    }
  },

  methods: {
    postPost() {
        axios.post(`http://jsonplaceholder.typicode.com/posts`, {
        body: this.email,
        body: this.password
        })
        .then(response => {})
        .catch(e => {
        this.errors.push(e)
        })
    }
  }
};
</script>
<style lang="scss" scoped>
#login {
  height: 50%;
  width: 100%;
  position: absolute;
  top: 0;
  left: 0;
  content: "";
  z-index: 0;
}
</style>
