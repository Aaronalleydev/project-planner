<template>
  <div class="home">
    <FilterNav @filterChange="current = $event" :current="current"/>
    <div v-if="projects.length" >
      <div v-for="project in filtered" :key="project.id" >
        <SingleProject :project="project" @delete="handleDelete" @complete="projectComplete"/>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import SingleProject from '../components/SingleProject.vue'
import FilterNav from '../components/FilterNav.vue'

export default {
  name: 'Home',
  components: { SingleProject, FilterNav },
  data() {
    return {
      projects: [],
      current: 'all'
    }
  },
  mounted() {
    fetch('http://localhost:3000/projects')
    .then(res => res.json())
    .then(data => this.projects = data)
    .catch(err => console.log(err.message))
  },
  methods: {
    handleDelete(id) {
      this.projects = this.projects.filter((project) => {
        return project.id !== id
      })
    },
    projectComplete(id) {
      let p = this.projects.find(project => {
        return project.id === id
      })

      p.complete = !p.complete
      
    },
  },
  computed: {
    filtered() {
      if (this.current === 'complete') {
        return this.projects.filter(project => project.complete)
      }
      if (this.current === 'uncomplete') {
        return this.projects.filter(project => !project.complete)
      }
      return this.projects
    }
  }
}
</script>
