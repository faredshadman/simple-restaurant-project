<template>
  <div class="login-wrap">
    <img src="../assets/resto-logo.jpg" alt="Logo" class="logo" />
    <h1>Login</h1>
    <div class="login">
      <input type="email" placeholder="Your Email" v-model="email" />
      <input type="password" placeholder="Your Password" v-model="password" />
      <button @click="login">Login</button>
      <p>
        <router-link to="/sign-up"> Sign Up </router-link>
      </p>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "LoginView",
  data() {
    return {
      email: "",
      password: "",
    };
  },
  mounted() {
    let user = localStorage.getItem("user-info");
    if (user) {
      this.$router.push({ name: "HomeView" });
    }
  },
  methods: {
    async login() {
      let result = await axios.get(
        `http://localhost:3000/users?email=${this.email}&password=${this.password}`
      );
      console.log(result.data);
      if (result.status == 200 && result.data.length > 0) {
        localStorage.setItem("user-info", JSON.stringify(result.data[0]));
        this.$router.push({ name: "HomeView" });
      }
    },
  },
};
</script>
