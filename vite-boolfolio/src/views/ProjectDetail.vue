<template>
    <div v-if="project" class="project-detail">
      <h1>{{ project.titolo }}</h1>
      <p>{{ project.descrizione }}</p>
      <div v-if="project.type">
        <h2>Type</h2>
        <p>{{ project.type.name }}</p>
      </div>
      <div v-if="project.technologies.length">
        <h2>Technologies</h2>
        <ul>
          <li v-for="tech in project.technologies" :key="tech.id">{{ tech.name }}</li>
        </ul>
      </div>
    </div>
    <div v-else>
      <p>Loading...</p>
    </div>
  </template>
  
  <script>
  import axios from '../axios';
  
  export default {
    name: 'ProjectDetail',
    data() {
      return {
        project: null
      };
    },
    props: {
      id: {
        type: String,
        required: true
      }
    },
    mounted() {
      this.fetchProject();
    },
    methods: {
      fetchProject() {
        axios.get(`/projects/${this.id}`)
          .then(response => {
            this.project = response.data;
          })
          .catch(error => {
            console.error("Error fetching project:", error);
          });
      }
    }
  };
  </script>
  
  <style scoped>
  .project-detail {
    padding: 20px;
  }
  </style>
  