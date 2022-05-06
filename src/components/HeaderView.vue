<template>
  <nav class="nav">
    <router-link to="/">Home</router-link>
    <router-link to="/add-rest">Add Restaurant</router-link>
    <a href="#" @click="logout">Logout</a>
  </nav>
</template>

<script>
export default {
  name: "HeaderView",
  mounted() {
    let result = localStorage.getItem("user-info");
    return result;
  },
  methods: {
    logout() {
      localStorage.removeItem("user-info");
      this.$router.push({
        name: "LoginView",
      });
    },
  },
};
</script>

<style scoped>
.nav {
  background: #333;
  overflow: hidden;
}
.nav a {
  display: inline-block;
  padding: 16px;
  text-decoration: none;
  color: #fff;
  text-align: center;
  font-size: 18px;
  transition: 0.4s;
}
.nav a:hover {
  background: #ddd;
  color: #000;
  border-radius: 0px 8px 0px 8px;
}
</style>
