<template>
  <div class="row">
    <div class="container">
      <h1>Login</h1>
      <hr />
    </div>

    <div v-if="errors" class="col s12 m7">
      <div class="card horizontal">
        <div class="card-stacked">
          <div class="card-content">
            <p class="red-text">Email / Password error</p>
          </div>
        </div>
      </div>
    </div>
    <form @submit.prevent="validateRegister" class="col s12">
      <div class="row">
        <div class="input-field col s12">
          <input
            id="email"
            type="email"
            class="validate"
            v-model.trim="email"
          />
          <label for="email">Email</label>
        </div>
      </div>
      <div class="row">
        <div class="input-field col s12">
          <input
            id="password"
            type="password"
            class="validate"
            v-model.trim="password"
          />
          <label for="password">Password</label>
        </div>
      </div>

      <button
        class="btn waves-effect waves-light blue darken-3"
        type="submit"
        name="action"
      >
        Login
      </button>
    </form>
  </div>
</template>

<script>
import router from "../router/index";

export default {
  data: () => ({
    email: "",
    password: "",
    errors: false,
  }),
  methods: {
    async validateRegister() {
      if (this.email !== "" && this.password.length > 5) {
        const API_KEY = "AIzaSyBXhLZeP0c2l4wmsMDp-C3Li81ZLVaoAPQ";
        const response = await fetch(
          `https://identitytoolkit.googleapis.com/v1/accounts:signInWithPassword?key=${API_KEY}`,
          {
            method: "POST",
            body: JSON.stringify({
              email: this.email,
              password: this.password,
              returnSecureToken: true,
            }),
          }
        );
        const data = await response.json();
        console.log(data);
        if (data.error !== undefined) {
          this.errors = true;
        } else {
          // this.errors = false;
          localStorage.setItem("userData", JSON.stringify(data));
          router.push("/projects");
        }
        console.log(data);
      } else {
        return;
      }
    },
  },
};
</script>
