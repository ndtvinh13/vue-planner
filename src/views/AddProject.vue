<template>
  <form @submit.prevent="handleSubmit">
    <label>Title:</label>
    <input type="text" v-model="title" required />
    <label>Details:</label>
    <textarea id="" cols="30" rows="10" v-model="details" required></textarea>
    <button>Add Project</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      title: "",
      details: "",
      uri: "http://localhost:3000/projects",
    };
  },

  methods: {
    handleSubmit() {
      console.log(this.title, this.details);
      let project = {
        title: this.title,
        details: this.details,
        complete: false,
      };

      fetch(this.uri, {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(project),
      })
        .then(() => {
          // Do somethind when the fetch is complete
          this.$router.push("/"); //Redirect to home page
        })
        .catch((err) => console.log(err.message));
    },
  },
};
</script>

<style>
form {
  background: #fff;
  padding: 20px 30px;
  border-radius: 10px;
  margin: auto;
  box-shadow: rgba(0, 0, 0, 0.24) 0px 3px 8px;
}

label {
  display: block;
  color: #333;
  text-transform: uppercase;
  font-weight: bold;
  margin: 20px 0 10px 0;
  letter-spacing: 1px;
}

input {
  padding: 10px;
  border: none;
  border-bottom: 2px solid #ddd;
  width: 100%;
  box-sizing: border-box;
}

textarea {
  padding: 10px;
  border: 2px solid #ddd;
  width: 100%;
  border-radius: 10px;
  box-sizing: border-box;
}

button {
  display: block;
  padding: 10px 20px;
  background: #00ce89;
  color: white;
  margin: 20px auto;
  border: none;
  border-radius: 5px;
  font-size: 16px;
}
</style>
