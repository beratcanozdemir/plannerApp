<template>
  <form @submit.prevent="projectSubmit">
    <label>Title:</label>
    <br />
    <input type="text" v-model="title" required />
    <br />
    <label>Details:</label>
    <br />
    <textarea v-model="details" required></textarea>
    <br />
    <button>Add Project</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      title: "",
      details: "",
    };
  },
  methods: {
    projectSubmit() {
      let newProject = {
        title: this.title,
        details: this.details,
        complete: false,
      };
      fetch("http://localhost:3000/projects", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(newProject),
      })
        .then(() => this.$router.push("/homePage"))
        .catch((err) => console.log(err.name));
    },
  },
};
</script>

<style>
form {
  background-color: white;
  padding: 20px;
  margin-top: 20px;
  border-radius: 10px;
}
label {
  display: block;
  color: #bbb;
  font-size: 15px;
  font-weight: bold;
  text-transform: uppercase;
  letter-spacing: 1px;
  margin: 20px 0 10px 0;
}
input {
  padding: 10px;
  border: 2px solid #ddd;
  width: 100%;
  box-sizing: border-box;
}
textarea {
  padding: 10px;
  border: 2px solid #ddd;
  width: 100%;
  height: 100px;
  box-sizing: border-box;
}
form button {
  display: block;
  margin: 20px auto 0;
  background-color: green;
  color: white;
  padding: 10px;
  border: 0;
  border-radius: 10px;
  font-size: 15px;
  cursor: pointer;
}
</style>
