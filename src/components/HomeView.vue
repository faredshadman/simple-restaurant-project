<template>
  <HeaderView />
  <div class="home">
    <h1>Hello {{ name }},Welcome on Home Page</h1>
    <table border="1">
      <thead>
        <th>ID</th>
        <th>Name</th>
        <th>Address</th>
        <th>Contact</th>
        <th>Actions</th>
      </thead>
      <tbody>
        <tr v-for="item in restaurant" :key="item.id">
          <td>
            {{ item.id }}
          </td>
          <td>
            {{ item.name }}
          </td>
          <td>
            {{ item.address }}
          </td>
          <td>
            {{ item.contact }}
          </td>
          <td>
            <router-link :to="'/upd-rest/' + item.id">Update</router-link>
            <button @click="deleteRestaurant(item.id)">Delete</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import HeaderView from "./HeaderView.vue";
import axios from "axios";
export default {
  name: "HomeView",
  components: {
    HeaderView,
  },
  data() {
    return {
      name: "",
      restaurant: [],
    };
  },
  async mounted() {
    this.loadData();
  },
  methods: {
    async deleteRestaurant(id) {
      let result = await axios.delete("http://localhost:3000/restaurant/" + id);
      if (result.status === 200) {
        this.loadData();
      }
    },
    async loadData() {
      let user = localStorage.getItem("user-info");
      this.name = JSON.parse(user).name;
      if (!user) {
        this.$router.push({ name: "SignUp" });
      }
      let result = await axios.get("http://localhost:3000/restaurant");
      this.restaurant = result.data;
    },
  },
};
</script>

<style scoped>
.home {
  padding-top: 2rem;
  text-align: center;
}
table {
  margin: 2rem auto;
}
td {
  width: 160px;
  height: 40px;
}
</style>
