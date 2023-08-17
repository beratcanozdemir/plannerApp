<template>
  <div class="homePage">
    <FilterNav @filterChange="current = $event" :current="current"></FilterNav>
    <div v-if="projects.length">
      <div v-for="project in filteredProjects" :key="project.id">
        <SingleProject
          :project="project"
          @delete="deleteMethod"
          @complete="completeMethod"
        ></SingleProject>
        <Navbar />
      </div>
    </div>
  </div>
</template>

<script>
import SingleProject from "../components/SingleProject.vue";
import FilterNav from "../components/FilterNav.vue";
export default {
  name: "HomePage",
  components: { SingleProject, FilterNav },
  data() {
    return {
      projects: [],
      current: "all",
    };
  },
  mounted() {
    fetch("http://localhost:3000/projects")
      .then((res) => res.json())
      .then((data) => (this.projects = data))
      .catch((err) => console.log(err.message));
  },
  methods: {
    deleteMethod(id) {
      this.projects = this.projects.filter((project) => project.id !== id);
    },
    completeMethod(id) {
      let c = this.projects.find((project) => project.id === id);
      c.complete = !c.complete;
    },
  },
  computed: {
    filteredProjects() {
      if (this.current === "completed") {
        return this.projects.filter((project) => project.complete);
      } else if (this.current === "ongoing") {
        return this.projects.filter((project) => !project.complete);
      } else {
        return this.projects;
      }
    },
  },
};
</script>
