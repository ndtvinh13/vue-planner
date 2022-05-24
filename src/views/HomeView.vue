<template>
  <div class="home">
    <FilterNav @filterChange="current = $event" :current="current" />
    <!-- if there is data -->
    <div v-if="projects.length">
      <div v-for="project in filteredProject" :key="project.id">
        <SingleProject
          :project="project"
          @delete="handelDelete"
          @complete="handleComplete"
        />
      </div>
    </div>
    <!-- If there is no data -->
    <!-- <div v-else>There is no projects !!</div> -->
  </div>
</template>

<script>
import SingleProject from "../components/SingleProject.vue";
import FilterNav from "../components/FilterNav.vue";

export default {
  name: "Home",

  components: { SingleProject, FilterNav },

  data() {
    return {
      projects: [],
      current: "all",
    };
  },

  mounted() {
    // fetch the data when the component is mounted to DOM
    fetch("http://localhost:3000/projects")
      .then((res) => res.json())
      .then((data) => (this.projects = data))
      .catch((err) => console.log(err.message));
  },

  methods: {
    handelDelete(id) {
      // Use filter method to get the id
      // "this.projects = " to update the object
      this.projects = this.projects.filter((project) => {
        return project.id !== id;
      });
    },

    handleComplete(id) {
      // find the project that matches the id
      let p = this.projects.find((project) => {
        return project.id === id;
      });

      p.complete = !p.complete;
    },
  },

  computed: {
    filteredProject() {
      if (this.current === "completed") {
        return this.projects.filter((project) => project.complete);
      }
      if (this.current === "ongoing") {
        return this.projects.filter((project) => !project.complete);
      }
      return this.projects;
    },
  },
};
</script>

<style>
.home {
  font-size: 25px;
}
</style>
