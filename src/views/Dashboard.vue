<template>
  <div class="dashboard container">
<h1>Welcome {{ user.username }}</h1>
    <div class="container" v-if="user.username === 'admin'">
      <table class="">
          <caption>User Details</caption>
        <thead>
          <tr>
            <th>ID</th>
            <th>Username</th>
            <th>Email</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(item, index) in users" :key="item.username">
            <td data-label="ID">{{ index + 1 }}</td>
            <td data-label="Username">{{ item.username }}</td>
            <td data-label="Email">{{ item.email }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      user: "",
      users: [],
    };
  },
  mounted() {
    if (localStorage.activeUser) {
      let lsUsers = localStorage.users;
      this.users = JSON.parse(lsUsers);

      let activeUser = localStorage.activeUser;
      this.user = JSON.parse(activeUser);
    }
  },
};
</script>

<style></style>
