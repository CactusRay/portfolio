<template>
  <main id="main-content">
    <HeroSection />
    <PostsList />
    <ProjectsGrid />
    <GithubProjects />
  </main>
</template>

<script setup>
defineOptions({ name: 'HomePage' })
import { onMounted } from 'vue'
import lozad from 'lozad'
import config from '@/config/siteconfig.json'

const { siteName: title } = config
const { description } = config

const route = useRoute()

useHead({
  title,
  meta: [
    {
      name: 'description',
      content: description,
    },
    { property: 'og:type', content: 'website' },
    { property: 'og:title', content: title },
    { property: 'og:description', content: description },
    { property: 'og:url', content: `${config.siteUrl}${route.path}` },
    {
      property: 'twitter:title',
      content: title,
    },
    {
      property: 'twitter:description',
      content: description,
    },
  ],
})

onMounted(() => {
  const observer = lozad('.lozad', { threshold: 0.2, })
  observer.observe()
})
</script>
