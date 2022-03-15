<template>
  <div>
    <nav>
      <div class="nav-wrapper blue lighten-1">
        <router-link to="/" class="brand-logo">Projects</router-link>
        <a href="#" data-target="mobile-demo" class="sidenav-trigger"
          ><i class="material-icons">menu</i></a
        >
        <ul class="right hide-on-med-and-down">
          <li>
            <router-link to="/" v-if="!checkSession">Register</router-link>
          </li>
          <li>
            <router-link
              to="/projects"
              class="waves-effect waves-light btn blue darken-3"
              v-if="checkSession"
              >Projects
            </router-link>
          </li>
          <li>
            <router-link
              to="/"
              class="waves-effect waves-light btn blue darken-3"
              v-if="checkSession"
              @click="closeSession"
              >Logout
            </router-link>
          </li>
          <li>
            <router-link to="/login" v-if="!checkSession">Login</router-link>
          </li>
        </ul>
      </div>
    </nav>

    <ul class="sidenav" id="mobile-demo">
      <li>
        <router-link to="/" v-if="!checkSession">Register</router-link>
      </li>
      <li>
        <router-link to="/projects" v-if="checkSession">Projects</router-link>
      </li>
      <li>
        <router-link to="/" v-if="checkSession" @click="closeSession">Logout</router-link>
      </li>
      <li>
        <router-link to="/login" v-if="!checkSession">Login</router-link>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  mounted() {
    M.AutoInit();
  },

  methods: {
    closeSession() {
      const user = localStorage.getItem("userData");
      if (user) {
        localStorage.removeItem("userData");
      }
    }
  },

  computed: {
    checkSession() {
      const user = localStorage.getItem("userData");
      if (user) {
        return true;
      }
    },
  },
};
</script>

<style></style>
