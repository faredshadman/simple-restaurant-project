<template>
  <HeaderView />
  <main class="add-wrap">
    <h1>Add</h1>
    <form class="add">
      <input
        type="text"
        name="name"
        id="name"
        placeholder="Enter Name"
        v-model="restaurant.name"
      />
      <input
        type="text"
        name="address"
        id="address"
        placeholder="Enter Address"
        v-model="restaurant.address"
      />
      <input
        type="text"
        name="contact"
        id="contact"
        placeholder="Enter Contact"
        v-model="restaurant.contact"
      />
      <button type="button" @click="addRestaurant">Add new restaurant</button>
    </form>
  </main>
</template>

<script>
import HeaderView from "./HeaderView.vue";
import axios from "axios";
export default {
  name: "AddView",
  components: {
    HeaderView,
  },
  mounted() {
    let user = localStorage.getItem("user-info");
    if (!user) {
      this.$router.push({ name: "SignUp" });
    }
  },
  data() {
    return {
      restaurant: {
        name: "",
        address: "",
        contact: "",
      },
    };
  },
  methods: {
    async addRestaurant() {
      const newRest = {
        name: this.restaurant.name,
        address: this.restaurant.address,
        contact: this.restaurant.contact,
      };
      const result = await axios.post(
        "http://localhost:3000/restaurant",
        newRest
      );
      if (result.status == 201) {
        this.$router.push({ name: "HomeView" });
      }
    },
  },
};
</script>

<style scoped></style>
