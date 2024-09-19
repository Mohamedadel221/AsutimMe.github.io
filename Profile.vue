<template>
  <div class="container">
    <Navbar />
  </div>
  <h2 class="text-capitalize">Update your profile</h2>
  <div class="parent-update-profile">
    <v-container>
      <v-sheet class="mx-auto" width="300">
        <v-form @submit.prevent>
          <div class="name">
            <v-text-field
              disabled
              type="text"
              label="Name"
              variant="outlined"
              elevation="0"
              color="green"
              v-model="name"
            >
            </v-text-field>
          </div>
          <div class="email">
            <v-text-field
              disabled
              type="email"
              label="Email"
              variant="outlined"
              elevation="0"
              color="green"
              v-model="email"
              rounded="1"
            >
            </v-text-field>
          </div>
          <div class="password">
            <v-text-field
              disabled
              type="password"
              label="Password"
              variant="outlined"
              elevation="0"
              color="green"
              v-model="pass"
            >
            </v-text-field>
          </div>
          <div class="btn">
            <v-btn
              @click="updateProfileNow()"
              class="mr-5 text-capitalize"
              type="submit"
              color="green"
              elevation="0"
              >update profile</v-btn
            >
          </div>
        </v-form>
      </v-sheet>
    </v-container>
  </div>
</template>
<script>
import { mapActions } from "vuex";
import Navbar from "./Navbar.vue";
export default {
  name: "profile-page",
  components: {
    Navbar,
  },
  data() {
    return {
      name: "",
      email: "",
      pass: "",
    };
  },
  mounted() {
    let user = localStorage.getItem("user-info");
    if (user) {
      this.name = JSON.parse(user).name;
      this.email = JSON.parse(user).emai;
      this.pass = JSON.parse(user).pass;
    } else {
      this.redirectTo({ val: "signup" });
    }
  },
  methods: {
    ...mapActions(["redirectTo"]),
    updateProfileNow() {
      this.redirectTo({ val: "update-profile" });
    },
  },
};
</script>
<style scoped lang="scss"></style>
