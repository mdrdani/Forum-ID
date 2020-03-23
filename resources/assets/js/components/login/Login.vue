<template>
  <v-container>
    <v-card class="pa-md-4 mx-lg-auto" color="white" width="500px">
      <v-form @submit.prevent="login">
        <v-text-field v-model="form.email" label="E-mail" type="email" required></v-text-field>

        <v-text-field v-model="form.password" label="Password" type="password" required></v-text-field>

        <v-btn color="green" type="submit">Login</v-btn>

        <router-link to="/signup">
          <v-btn color="blue">Sign Up</v-btn>
        </router-link>
      </v-form>
    </v-card>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      form: {
        email: null,
        password: null
      }
    };
  },
  created() {
    if (User.loggedIn()) {
      this.$router.push({ name: "forum" });
    }
  },
  methods: {
    login() {
      User.login(this.form);
    }
  }
};
</script>

<style lang="">
</style>