<template>
  <div class="project" :class="{complete: project.complete}">
    <div class="actions">
      <h2 @click="showDetails = !showDetails">{{ project.title }}</h2>
      <div class="icons">
        <span class="material-icons tick" @click="projectDone"> done </span>
        <router-link :to="{ name: 'EditProject', params: {id: project.id}}">
            <span class="material-icons"> edit </span>
        </router-link>
        <span class="material-icons" @click="deleteProject"> delete </span>
      </div>
    </div>
    <div class="details" v-if="showDetails">
      {{ project.details }}
    </div>
  </div>
</template>

<script>
export default {
  props: ["project"],
  data() {
    return {
      showDetails: false,
      url: 'http://localhost:3000/projects/' + this.project.id
    };
  },
  methods: {
      deleteProject(){
          fetch(this.url, { method: "DELETE"})
            .then((res) => this.$emit('delete', this.project.id))
            .catch((err) => console.log(err))
      },

      projectDone(){
        this.project.complete = !this.project.complete
        fetch(this.url, { 
              method: "PATCH",
              headers: { "Content-Type": "application/json" },
              body: JSON.stringify({
                  complete: this.project.complete
              })
        })
            .then((res) => this.$emit('complated', this.project.id))
            .catch((err) => console.log(err))
      }
  },
};
</script>

<style>
.project {
  margin: 20px auto;
  background: white;
  padding: 10px 20px;
  border-radius: 4px;
  box-shadow: 1px 2px 3px rgba(0, 0, 0, 0.05);
  border-left: 4px solid #e90074;
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
  font-size: 24px;
  margin-left: 10px;
  color: #bbb;
  cursor: pointer;
}
.material-icons:hover {
  color: #777;
}

/* Complated Projects */

.project.complete{
    border-left: 4px solid #00ce89;
}

.project.complete  .tick{
    color: #00ce89;
}
</style>


