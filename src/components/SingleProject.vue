<template>
  <div class="project" :class="{ complete: project.complete }">
    <div class="actions">
      <h3 @click="showDetails = !showDetails">{{ project.title }}</h3>
      <div class="icons">
        <router-link :to="{ name: 'EditProject', params: { id: project.id } }">
          <span class="material-symbols-outlined"> edit </span>
        </router-link>
        <span class="material-symbols-outlined" @click="deleteProject">
          delete
        </span>
        <span
          class="material-symbols-outlined"
          @click="toggleComplete"
          :class="{ check: project.complete }"
        >
          done
        </span>
      </div>
    </div>
    <div class="details" v-if="showDetails">{{ project.details }}</div>
  </div>
</template>

<script>
export default {
  props: ["project"],

  data() {
    return {
      showDetails: false,
      uri: "http://localhost:3000/projects/" + this.project.id,
    };
  },

  methods: {
    deleteProject() {
      fetch(this.uri, { method: "DELETE" }).then(() =>
        this.$emit("delete", this.project.id).catch((err) =>
          console.log(err.message)
        )
      );
    },

    toggleComplete() {
      fetch(this.uri, {
        method: "PATCH",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ complete: !this.project.complete }), //stringify
      })
        .then(() => this.$emit("complete", this.project.id))
        .catch((err) => console.log(err.message));
    },
  },
};
</script>

<style>
.project {
  margin: 20px auto;
  background: #fff;
  padding: 20px 20px;
  font-size: 20px;
  border-radius: 4px;
  border-left: 5px solid #e90074;
  box-shadow: rgba(0, 0, 0, 0.24) 0px 3px 8px;
  transition: 0.3s;
}

.project:hover {
  box-shadow: rgba(0, 0, 0, 0.3) 0px 5px 9px;
}

.complete {
  border-left: 5px solid #3aa776;
}

.check {
  color: rgb(9, 218, 218) !important;
}

h3 {
  margin: 15px 0;
  cursor: pointer;
}

.details {
  margin: 15px 0;
}

.actions {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
}

.icons span {
  cursor: pointer;
  margin-right: 6px;
  transition: 0.3s;
}

.icons span:first-child:hover {
  color: #777;
}

.icons span:nth-child(2) {
  color: crimson;
  transition: 0.3s;
}

.icons span:nth-child(2):hover {
  color: rgb(253, 33, 77);
}

.icons span:nth-child(3) {
  color: #3aa776;
  transition: 0.3s;
}

.icons span:nth-child(3):hover {
  color: #44d493;
}
</style>
