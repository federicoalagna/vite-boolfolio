<template>
  <div id="app">
    <h1>Progetti</h1>
    <div v-if="loading">Caricamento...</div>
    <div v-if="error">{{ error }}</div>
    <div v-if="projects.length">
      <ProjectCard v-for="project in projects" :key="project.id" :project="project" />
    </div>
  </div>
</template>

<script>
import axios from './axios';
import ProjectCard from './components/ProjectCard.vue';

export default {
  name: 'App',
  components: {
    ProjectCard
  },
  data() {
    return {
      projects: [],
      loading: true,
      error: null
    };
  },
  mounted() {
    axios.get('/projects')
      .then(response => {
        this.projects = response.data;
        this.loading = false;
      })
      .catch(error => {
        this.error = 'Errore durante il caricamento dei progetti';
        this.loading = false;
      });
  }
};
</script>
