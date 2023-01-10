<template>
  <div class="home">
    <FilterProject @filterChange="current = $event" :current="current" @click="filterProject"/>
    <div v-if="projects.length">
      <div v-for="project in filterProject" :key="project.id">
        <SingleProject :project="project"  @delete="handleDelete" @complated="handleComplate"/>
      </div>
    </div>
  </div>
</template>

<script>
import SingleProject from "../components/SingleProject.vue";
import FilterProject from '../components/FilterProject.vue'

export default {
  name: "HomeView",
  components: {
    SingleProject,
    FilterProject
  },
  data() {
    return {
      projects: [],
      current: 'all'
    }
  },
  mounted() {
    fetch("http://localhost:3000/projects")
      .then((res) => res.json())
      .then((data) => (this.projects = data))
      .catch((err) => console.log(err.message));
  },
  methods: {
    handleDelete(id){
      console.log(id);
      this.projects = this.projects.filter((project) =>{
        return project.id !== id;
      })
    },

    handleComplate(id){
      let pro = this.projects.filter((project) => {
        return project.id !== id;
      })
      pro.complete = !pro.complete;
    }
  },

  computed: {
    filterProject(){
      if(this.current === 'complated'){
        return this.projects.filter((project) => project.complete)
      }

      if(this.current === 'ongoing'){
        return this.projects.filter((project) => !project.complete)
      }

      return this.projects
    }
  }
};
</script>
