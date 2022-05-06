<template>
  <div class="signup-wrap">
    <img src="../assets/resto-logo.jpg" alt="Logo" class="logo" />
    <h1>SignUp</h1>
    <div class="register">
      <input type="text" placeholder="Your Name" v-model="name" />
      <input type="email" placeholder="Your Email" v-model="email" />
      <input type="password" placeholder="Your Password" v-model="password" />
      <button @click="signUp">Sign Up</button>
      <p>
        <router-link to="/login"> Login </router-link>
      </p>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "SignUp",
  data() {
    return {
      name: "",
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
    async signUp() {
      let result = await axios.post("http://localhost:3000/users", {
        name: this.name,
        email: this.email,
        password: this.password,
      });
      console.log(result);
      if (result.status == 201) {
        localStorage.setItem("user-info", JSON.stringify(result.data));
        this.$router.push({ name: "HomeView" });
      }
    },
  },
};
</script>

<style>
.signup-wrap,
.login-wrap,
.add-wrap {
  padding-top: 2rem;
  text-align: center;
}
.signup-wrap h1,
.login-wrap h1,
.add-wrap h1 {
  padding-bottom: 2rem;
}
.logo {
  width: 100px;
  margin-bottom: 1rem;
}
.register input,
.login input,
.add input {
  width: 300px;
  height: 40px;
  display: block;
  padding-left: 20px;
  margin-bottom: 30px;
  margin-right: auto;
  margin-left: auto;
  border: 1px solid skyblue;
}
.register button,
.login button,
.add button {
  width: 300px;
  height: 40px;
  border: 1px solid skyblue;
  background: skyblue;
  color: #fff;
  cursor: pointer;
}
</style>
