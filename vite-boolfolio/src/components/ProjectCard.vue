<template>
    <div class="project-card">
      <h2>{{ project.titolo }}</h2>
      <p>{{ project.descrizione }}</p>
    </div>
  </template>
  
  <script>
  export default {
    name: 'ProjectCard',
    props: {
      project: {
        type: Object,
        required: true
      }
    }
  };
  </script>
  
  <style scoped>
  .project-card {
    border: 1px solid #ccc;
    padding: 16px;
    margin: 16px;
    border-radius: 8px;
  }
  </style>
  