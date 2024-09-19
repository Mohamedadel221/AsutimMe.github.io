<template>
  <div class="parent-sign-in">
    <v-container>
      <v-sheet class="mx-auto" width="300">
        <v-form @submit.prevent>
          <h2 class="text-capitalize">Sign Up</h2>
          <div class="name">
            <v-text-field
              type="text"
              label="Name"
              variant="outlined"
              elevation="0"
              color="green"
              v-model="name"
            >
            </v-text-field>
            <span class="error-feedback" v-if="v$.name.$error">{{
              v$.name.$errors[0].$message
            }}</span>
          </div>
          <div class="email">
            <v-text-field
              type="email"
              label="Email"
              variant="outlined"
              elevation="0"
              color="green"
              v-model="email"
              rounded="1"
            >
            </v-text-field>
            <span class="error-feedback" v-if="v$.email.$error">{{
              v$.email.$errors[0].$message
            }}</span>
          </div>
          <div class="password">
            <v-text-field
              type="password"
              label="Password"
              variant="outlined"
              elevation="0"
              color="green"
              v-model="pass"
            >
            </v-text-field>
            <span class="error-feedback" v-if="v$.pass.$error">{{
              v$.pass.$errors[0].$message
            }}</span>
          </div>
          <div class="btn">
            <v-btn
              @click="signUpNow()"
              class="mr-5 text-capitalize"
              type="submit"
              color="green"
              elevation="0"
              >sign In</v-btn
            >
            <v-btn
              class="mr-5 text-capitalize"
              type="button"
              color="green"
              variant="outlined"
              @click="redirectTo({ val: 'log-in' })"
              >Log In</v-btn
            >
          </div>
          <div class="user-not-found">
            <h2 class="not-found-error">{{ userNotFound }}</h2>
          </div>
        </v-form>
      </v-sheet>
    </v-container>
  </div>
</template>
<script>
import axios from "axios";
import { mapActions } from "vuex";
import useVuelidate from "@vuelidate/core";
import { required, email, minLength } from "@vuelidate/validators";
export default {
  name: "SignUpForm",
  data() {
    return {
      v$: useVuelidate(),
      name: "",
      pass: "",
      email: "",
    };
  },
  validations() {
    return {
      name: { required, minLength: minLength(0) },
      pass: { required, minLength: minLength(8) },
      email: { required, email },
    };
  },
  mounted() {
    let user = localStorage.getItem("user-info");
    if (user) {
      this.redirectTo({ val: "home" });
    }
  },
  methods: {
    ...mapActions(["redirectTo"]),
    async signUpNow() {
      this.v$.$validate();
      {
        if (!this.v$.$error) {
          console.log("Data Is Completed");
          let result = await axios.post("http://localhost:3000/user", {
            name: this.name,
            email: this.email,
            pass: this.pass,
          });
          if (result.status == 201) {
            // saveData In Local Storege //
            localStorage.setItem("user-info", JSON.stringify(result.data));
            // redircet to  //
            this.redirectTo({ val: "home" });
          } else {
            console.log("Added Users Not Completed");
          }
        }
      }
    },
  },
};
</script>
<style scoped>
.error-feedback {
  color: red;
  font-size: 12px;
  transition: 0.5s;
}
.parent-sign-in {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 80vh;
}
</style>
