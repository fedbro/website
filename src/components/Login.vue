<template>
  <div class="login">
    <div class="container flex login__container">
      <div class="card">
           <form novalidate @submit.prevent="loginUser">
        <div class="row">
          <label for="email">Email</label>
          <input
            type="text"
            :class="`form-control ${errors.username ? 'is-invalid' : ''}`"
            placeholder="Username"
            v-model="username"
          />
          <div class="invalid-feedback">{{ errors.username }}</div>
        </div>
        <div class="row">
          <label for="password">Password</label>
          <input
            type="password"
            :class="`form-control ${errors.password ? 'is-invalid' : ''}`"
            placeholder="Password"
            v-model="password"
          />
          <div class="invalid-feedback">{{ errors.password }}</div>
        </div>
        <button class="btn ">Login</button>
      </form>
      </div>
   
    </div>
  </div>
</template>

<script>
import validateLoginInput from "../validation/validateLoginInput";
export default {
  data() {
    return {
      username: "",
      password: "",
      errors: {},
    };
  },
  methods: {
    loginUser() {
      let credentials = {
        username: this.username,
        password: this.password,
      };

      const { isInvalid, errors } = validateLoginInput(credentials);

      if (isInvalid) {
        this.errors = errors;
      } else {
        this.errors = {};
        // login code goes here
        let lsUsers = localStorage.users;
        lsUsers = JSON.parse(lsUsers);
        let usernameIndex = lsUsers.findIndex(
          (user) => user.username === credentials.username
        );
        if (usernameIndex > -1) {
          let passwordIndex = lsUsers.findIndex(
            (user) => user.password === credentials.password
          );

          if (passwordIndex > -1) {
            let activeUser = lsUsers.find(
              (user) => user.username === credentials.username
            );
            localStorage.setItem("activeUser", JSON.stringify(activeUser));
            this.$router.push("/dashboard");
            window.location.reload();
          } else {
            this.errors.password = "Password does not match!";
          }
        } else {
          this.errors.username = "Username does not exist!";
        }
      }
    },
  },
};
</script>

<style>

</style>
