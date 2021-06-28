<template>
  <div class="register">
    <div class="container flex register__container">
       <div class="card">
              <form novalidate @submit.prevent="registerUser()">
                <div class="row">
                  <label for="name">User Name</label>
                  <input
                    type="text"
                    :class="`form-control ${
                      errors.username ? 'is-invalid' : ''
                    }`"
                    placeholder="Username"
                    v-model="username"
                  />
                  <div class="invalid-feedback">{{ errors.username }}</div>
                </div>
                <div class=" row">
                  <label for="email">Email</label>
                  <input
                    type="email"
                    :class="`form-control ${errors.email ? 'is-invalid' : ''}`"
                    placeholder="Email"
                    v-model="email"
                  />
                  <div class="invalid-feedback">{{ errors.email }}</div>
                </div>
                <div class="row">
                  <label for="password">password</label>
                  <input
                    type="password"
                    :class="`form-control ${
                      errors.password ? 'is-invalid' : ''
                    }`"
                    placeholder="Password"
                    v-model="password"
                  />
                  <div class="invalid-feedback">{{ errors.password }}</div>
                </div>
                <div class="row">
                  <label for="password">Confirm Password</label>
                  <input
                    type="password"
                    :class="`form-control ${
                      errors.password2 ? 'is-invalid' : ''
                    }`"
                    placeholder="Confirm Password"
                    v-model="password2"
                  />
                  <div class="invalid-feedback">{{ errors.password2 }}</div>
                </div>
                <button class="">
                  Register
                </button>
              </form>
            </div>
    </div>
  </div>
</template>

<script>
import validateRegisterInput from "../validation/validateRegisterInput";
export default {
  data() {
    return {
      username: "",
      email: "",
      password: "",
      password2: "",
      errors: {},
      users: [],
    };
  },
  methods: {
    registerUser() {
      let user = {
        username: this.username,
        email: this.email,
        password: this.password,
        password2: this.password2,
      };

      const { isInvalid, errors } = validateRegisterInput(user);

      if (isInvalid) {
        this.errors = errors;
      } else {
        this.errors = {};
        // store user in local storage
        if (localStorage.users) {
          let lsUsers = localStorage.users;
          this.users = JSON.parse(lsUsers);
        }
        this.users.push(user);
        localStorage.setItem("users", JSON.stringify(this.users));
        this.username = "";
        this.email = "";
        this.password = "";
        this.password2 = "";
        this.$router.push("/login");
      }
    },
  },
};
</script>

<style>

</style>
