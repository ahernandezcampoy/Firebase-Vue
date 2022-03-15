<template>
  <div class="container">
    <div class="row">
      <router-link
        to="/projects"
        class="col s12 waves-effect waves-light btn blue darken-1"
      >
        <i class="material-icons"> arrow_back </i>
      </router-link>
    </div>
    <div class="row">
      <form @submit.prevent="updateProject" class="col s12">
        <div class="row">
          <div class="input-field col s6">
            <input
              placeholder="Title"
              id="project_title"
              type="text"
              class="validate"
              v-model="project.title"
            />
            <label for="project_title"></label>
          </div>
          <div class="input-field col s12">
            <input
              placeholder="Description"
              id="description"
              type="text"
              class="validate"
              v-model="project.description"
            />
            <label for="description"></label>
          </div>
        </div>
        <p>
          <label>
            <input type="checkbox" value="html" v-model="project.langs" />
            <span>HTML</span>
          </label>
        </p>
        <p>
          <label>
            <input type="checkbox" value="css" v-model="project.langs" />
            <span>CSS</span>
          </label>
        </p>
        <p>
          <label>
            <input type="checkbox" value="js" v-model="project.langs" />
            <span>JS</span>
          </label>
        </p>
        <p>
          <label>
            <input type="checkbox" value="vue" v-model="project.langs" />
            <span>Vue</span>
          </label>
        </p>
        <div class="row">
          <button
            class="btn waves-effect waves-light blue darken-3 col s12 l3"
            type="submit"
            name="action"
          >
            Submit
            <i class="material-icons right">send</i>
          </button>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      project: {
        title: "",
        description: "",
        langs: [],
        status: true,
      },
      id: this.$route.params.id,
    };
  },

  mounted() {
    this.getProject();
  },

  methods: {
    async getProject() {
      const userData = JSON.parse(localStorage.getItem("userData"));
      const response = await fetch(
        `https://crud-vue-8f4ff-default-rtdb.europe-west1.firebasedatabase.app/projects/${userData.localId}/${this.id}.json?auth=${userData.idToken}`
      );
      this.project = await response.json();

      console.log(this.project);
    },

    async updateProject() {
      const userData = JSON.parse(localStorage.getItem("userData"));
      console.log(this.project);
      await fetch(
        `https://crud-vue-8f4ff-default-rtdb.europe-west1.firebasedatabase.app/projects/${userData.localId}/${this.id}.json?auth=${userData.idToken}`,
        {
          method: "PATCH",
          body: JSON.stringify(this.project),
        }
      );
    },
  },
};
</script>
