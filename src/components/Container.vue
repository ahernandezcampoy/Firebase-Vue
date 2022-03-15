<template>
  <div class="row">
    <div class="col s12 m7">
      <card :content="project" v-for="(project, i) in projects" :key="i"></card>
    </div>
  </div>
</template>

<script>
import Card from "./Card.vue";
export default {
  data: () => ({
    projects: [],
  }),

  components: {
    Card,
  },

  mounted() {
    this.getProjects();
  },

  methods: {
    async getProjects() {
      const userData = JSON.parse(localStorage.getItem("userData"));
      console.log(userData);
      const response = await fetch(
        `https://crud-vue-8f4ff-default-rtdb.europe-west1.firebasedatabase.app/projects/${userData.localId}.json?auth=${userData.idToken}`
      );
      const data = await response.json();
      for (let i in data) {
        // Si no filtramos al añadir los elementos a "projects"
        // hay que añadir un v-if en la "Card"
        // if (data[i].status) {
        this.projects.push({
          id: i,
          value: data[i],
        });
        // }
      }

      console.log(this.projects);
    },
  },
};
</script>
