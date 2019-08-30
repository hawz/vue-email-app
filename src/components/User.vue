<template>
  <div class="user-head">
    <img :src="user.image" />

    <div class="user-name">
      <h5>{{ fullName }}</h5>
      <span class="email-address">{{ user.email }}</span>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      user: {
        firstName: "Albe",
        lastName: "Masia",
        email: "hawz@github.io",
        image: "https://avatars0.githubusercontent.com/u/2722532?s=50&v=4"
      }
    };
  },
  computed: {
    fullName() {
      return `${this.user.firstName} ${this.user.lastName}`;
    }
  }
};
</script>

<style>
</style>
