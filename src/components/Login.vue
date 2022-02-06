<template>
  <div class="container mt-4">
    <div class="row">
      <div class="col-sm-4 mx-auto">
        <form class="login" @submit.prevent="login">
          <div class="mb-3">
            <label for="exampleInputUsername1" class="form-label"
              >Username</label
            >
            <input
              required
              type="username"
              v-model="username"
              class="form-control"
              placeholder="Username"
              id="exampleInputUsername1"
            />
          </div>
          <div class="mb-3">
            <label for="exampleInputPassword1" class="form-label"
              >Password</label
            >
            <input
              required
              v-model="password"
              type="password"
              class="form-control"
              id="exampleInputPassword1"
              placeholder="Password"
            />
          </div>
          <div v-if="errorMessage" class="text-danger">{{ errorMessage }}</div>
          <button type="submit" class="btn btn-primary">Submit</button>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      username: "",
      password: "",
      errorMessage: "",
    };
  },
  methods: {
    login: function () {
      let username = this.username;
      let password = this.password;
      this.$store
        .dispatch("login", { login: username, password })
        .then(() => this.$router.push("/about"))
        .catch((err) => (this.errorMessage = err.message));
    },
  },
};
</script>