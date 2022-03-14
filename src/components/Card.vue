<template>
  <div class="card horizontal" v-if="content.value.status">
    <div class="card-stacked">
      <div class="card-content">
        <span class="card-title">{{ content.value.title }}</span>
        <p>
          {{ content.value.description }}
        </p>
        <p>
          Technologies:
          <span v-for="(lang, i) in content.value.langs" :key="i">
            {{
              i < content.value.langs.length - 1
                ? `${lang.toUpperCase()}, `
                : lang.toUpperCase()
            }}
          </span>
        </p>
      </div>
      <div class="card-action">
        <div class="row">
          <router-link
            :to="`/edit-project/${content.id}`"
            class="col s6 waves-effect waves-light btn orange lighten-2"
          >
            <i class="material-icons">create</i>
          </router-link>
          <button
            @click="deleteProject"
            class="col s6 waves-effect waves-light btn red lighten-1"
          >
            <i class="material-icons"> delete </i>
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    content: Object,
  },

  computed: {
    displayLangs() {},
  },

  methods: {
    async deleteProject() {
      const id = this.content.id;
      const response = await fetch(
        `https://crud-vue-8f4ff-default-rtdb.europe-west1.firebasedatabase.app/projects/${id}.json`,
        {
          method: "PATCH",
          body: JSON.stringify({ status: false }),
        }
      );
      const data = await response.json();
      this.content.value.status = data["status"];
      console.log(data);
    },
  },
};
</script>
