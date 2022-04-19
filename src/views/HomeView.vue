<template>
  <div class="home">
    <ProFilter @filterChange="current =$event" :current="current"/>
    <div v-if="projects.length">
      <ul v-for="p in filteredProjects" :key="p.id">
        <SingleProject
          :p="p"
          @delete="deleteTask"
          @complete="completeTask"
          @important="imoprtantTask"
        />

      </ul>
    </div>
  </div>
</template>

<script>
import SingleProject from "@/components/SingleProject.vue"
import ProFilter from "@/components/ProFilter.vue"

export default {
  name: "Home",
  components: { SingleProject ,ProFilter},
  data() {
    return {
      projects: [],
      current:['all']
    };
  },
  mounted() {
    fetch("http://localhost:3000/projects")
      .then((res) => res.json())
      .then((data) => (this.projects = data))
      .catch((err) => console.log(err.massage));
  },
  methods: {
    deleteTask(id) {
      this.projects = this.projects.filter((p) => {
        return p.id !== id;
      });
    },
    completeTask(id) {
      let dof = this.projects.find((p) => {
        return p.id === id;
      });
      dof.complete = !dof.complete;
    },
    imoprtantTask(id) {
      let imt = this.projects.find((p) => {
        return p.id === id;
      });
      imt.important = !imt.important;
    },
  },
  computed:{
    filteredProjects(){
      if (this.current === 'completed'){

      return this.projects.filter(p => p.complete)
      }
      if (this.current === 'ongoing'){

      return this.projects.filter(p => !p.complete)
      }
      if (this.current === 'important'){

      return this.projects.filter(p => p.important)
      }
      return this.projects
    }

  }
};
</script>
