<template>
  <nav class="navbar ">
    <div class="navbar__container container flex">
      <router-link class="navbar__brand" to="/">Logo</router-link>

      <div class="navbar__content">
        <ul class="navbar__nav ">
          <li class="navbar__item" v-if="!user">
            <router-link class="navbar__link" to="/register">Register</router-link>
          </li>
        
          <li class="navbar__item" v-if="!user">
            <router-link class="navbar__link" to="/login">Login</router-link>
          </li>
          <li class="navbar__item" v-if="user">
            <a class="navbar__link" href="" @click.prevent="logout">Logout</a>
          </li>
        </ul>
      </div>
    </div>
  </nav>
</template>

<script>
export default {
  data() {
    return {
      user: "",
    };
  },
  mounted() {
    if (localStorage.activeUser) {
      let activeUser = localStorage.activeUser;
      this.user = JSON.parse(activeUser);
    }
  },
  methods: {
    logout() {
      localStorage.removeItem("activeUser");
      this.$router.push("/login");
      window.location.reload();
    },
  },
};
</script>

<style></style>
