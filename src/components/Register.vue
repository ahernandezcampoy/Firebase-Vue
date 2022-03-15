<template>
  <div class="row">
    <div class="container">
      <h1>Register</h1>
      <hr />
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
      <div class="row">
        <div class="input-field col s12">
          <input
            id="confirm-password"
            type="password"
            class="validate"
            v-model.trim="confirmPassword"
          />
          <label for="confirm-password">Confirm password</label>
        </div>
      </div>

      <button
        class="btn waves-effect waves-light blue darken-3"
        type="submit"
        name="action"
      >
        Register
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
    confirmPassword: "",
  }),
  methods: {
    async validateRegister() {
      if (
        this.email !== "" &&
        this.password === this.confirmPassword &&
        this.password.length > 5
      ) {
        console.log("Contraseñas válidas");
        const API_KEY = "AIzaSyBXhLZeP0c2l4wmsMDp-C3Li81ZLVaoAPQ";
        const response = await fetch(
          `https://identitytoolkit.googleapis.com/v1/accounts:signUp?key=${API_KEY}`,
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
        localStorage.setItem("userData", JSON.stringify(data));
        router.push("/projects");
      } else {
        return;
      }
    },
  },
};
</script>
