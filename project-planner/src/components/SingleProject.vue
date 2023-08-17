<template>
  <div class="project" :class="{ complete: project.complete }">
    <div class="actions">
      <h3 @click="showDetail">{{ project.title }}</h3>
      <div class="icons">
        <router-link
          :to="{ name: 'EditProject', params: { id: project.id } }"
          ><span class="material-icons">edit</span></router-link
        >
        <span @click="projectDelete" class="material-icons">delete</span>
        <span @click="projectComplete" class="material-icons tick">done</span>
      </div>
    </div>
    <div v-if="showDetails" class="details">
      <p>{{ project.details }}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: ["project"],
  data() {
    return {
      showDetails: false,
      urlThis: "http://localhost:3000/projects/" + this.project.id,
    };
  },
  methods: {
    showDetail() {
      this.showDetails = !this.showDetails;
    },
    projectDelete() {
      fetch(this.urlThis, { method: "DELETE" }).then(() =>
        this.$emit("delete", this.project.id)
      );
    },
    projectComplete() {
      fetch(this.urlThis, {
        method: "PATCH",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ complete: !this.project.complete }),
      })
        .then(() => this.$emit("complete", this.project.id))
        .catch((err) => console.log(err.name));
    },
  },
};
</script>

<style>
.project {
  margin: 20px auto;
  background-color: white;
  padding: 10px 20px;
  border-radius: 5px;
  box-shadow: 1px 2px 3px rgba(0, 0, 0, 0.5);
  border-left: 10px solid red;
}
h3 {
  cursor: pointer;
}
.actions {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.material-icons {
  font-size: 25px;
  margin-left: 10px;
  font-weight: bold;
  cursor: pointer;
  color: #bbb;
}
.material-icons:hover {
  color: #777;
}
.project.complete {
  border-left: 10px solid green;
}
.project.complete .tick {
  color: green;
}
</style>
