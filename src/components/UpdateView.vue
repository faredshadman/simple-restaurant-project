<template>
  <HeaderView />
  <main class="add-wrap">
    <h1>Update</h1>
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
      <button type="button" @click="updateRestaurant">
        Add new restaurant
      </button>
    </form>
  </main>
</template>

<script>
import HeaderView from "./HeaderView.vue";
import axios from "axios";
export default {
  name: "UpdateView",
  components: {
    HeaderView,
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
  async mounted() {
    let user = localStorage.getItem("user-info");
    if (!user) {
      this.$router.push({ name: "SignUp" });
    }
    const result = await axios.get(
      `http://localhost:3000/restaurant/` + this.$route.params.id
    );
    this.restaurant = result.data;
  },
  methods: {
    async updateRestaurant() {
      const newRest = {
        name: this.restaurant.name,
        address: this.restaurant.address,
        contact: this.restaurant.contact,
      };
      const result = await axios.put(
        "http://localhost:3000/restaurant/" + this.$route.params.id,
        newRest
      );
      if (result.status == 200) {
        this.$router.push({ name: "HomeView" });
      }
    },
  },
};
</script>

<style lang="scss" scoped></style>
