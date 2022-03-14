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
            <router-link to="/">Home</router-link>
          </li>
          <li>
            <router-link to="/projects" class="waves-effect waves-light btn blue darken-3"
              >Projects</router-link
            >
          </li>
          <li>
            <router-link to="/about">About</router-link>
          </li>
        </ul>
      </div>
    </nav>

    <ul class="sidenav" id="mobile-demo">
      <li>
        <router-link to="/">Home</router-link>
      </li>
      <li>
        <router-link to="/projects">Projects</router-link
        >
      </li>
      <li>
        <router-link to="/about">About</router-link>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  mounted() {
    M.AutoInit();
  },
};
</script>

<style></style>
