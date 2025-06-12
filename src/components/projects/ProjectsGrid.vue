<template>
  <section id="projects" class="projects-grid container">
    <h3>{{ $t('projectsTitle') }}</h3>
    <ProjectCard
      v-for="project in highlightedProjects"
      :key="project.title[locale] || project.title"
      :thumbnail="project.thumbnail"
      :title="typeof project.title === 'object' ? project.title[locale] : project.title"
      :description="typeof project.description === 'object' ? project.description[locale] : project.description"
      :tags="project.tags"
      :github="project.github"
    />
  </section>
</template>

<script setup>
import { useI18n } from 'vue-i18n'
import projects from '@content/projects/projects.json'

const { locale } = useI18n()
const highlightedProjects = Object.values(projects).filter(
  (project) => project.pinned
)
</script>

<style scoped>
.projects-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(min(400px, 100%), 1fr));
  grid-gap: 1rem;
  margin-block-end: 4rem;

  h3 {
    grid-column: 1 / -1;
    text-transform: uppercase;
    margin-block-start: 2rem;
  }
}
</style>
