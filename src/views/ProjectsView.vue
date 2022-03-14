<template>
  <div class="container">
    <h1>Projects view</h1>
    <hr />
    <div class="row">
      <router-link
        to="/create-project"
        class="col s12 waves-effect waves-light btn blue darken-1"
      >
        <i class="material-icons"> add </i>
      </router-link>
    </div>
    <container></container>
  </div>
</template>

<script>
import Container from "../components/Container.vue";
export default {
  components: { Container },
};
</script>

<style></style>
