<template>
    <div>
      <h1>Progetti</h1>
      <div v-if="loading">Caricamento...</div>
      <div v-if="error">{{ error }}</div>
      <div v-if="projects.length">
        <ProjectCard v-for="project in projects" :key="project.id" :project="project" />
      </div>
      <div>
        <button @click="prevPage" :disabled="page === 1">Precedente</button>
        <button @click="nextPage" :disabled="!hasMore">Successivo</button>
      </div>
    </div>
  </template>
  
  <script>
  import axios from '../axios';
  import ProjectCard from '../components/ProjectCard.vue';
  
  export default {
    name: 'Home',
    components: {
      ProjectCard
    },
    data() {
      return {
        projects: [],
        loading: true,
        error: null,
        page: 1,
        hasMore: true
      };
    },
    mounted() {
      this.fetchProjects();
    },
    methods: {
      fetchProjects() {
        this.loading = true;
        axios.get(`/projects?page=${this.page}`)
          .then(response => {
            this.projects = response.data.data;
            this.hasMore = !!response.data.next_page_url;
            this.loading = false;
          })
          .catch(error => {
            this.error = 'Errore durante il caricamento dei progetti';
            this.loading = false;
          });
      },
      nextPage() {
        this.page++;
        this.fetchProjects();
      },
      prevPage() {
        if (this.page > 1) {
          this.page--;
          this.fetchProjects();
        }
      }
    }
  };
  </script>
  
  <style scoped>
  /* Styles here */
  </style>
  