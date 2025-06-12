<template>
  <section class="github-projects container">
    <h3>{{ $t('githubAchievements') }}</h3>
    <div class="github-repositories-scroll">
      <div class="project-card" v-for="(item, idx) in projects" :key="idx">
        <img :src="`/${item.thumbnail}`" :alt="$t(item.title)" class="project-card__image" />
        <div class="project-desc">
          <h5>{{ $t(item.title) }}</h5>
          <p v-if="item.description">{{ $t(item.description) }}</p>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
const projects = [
  {
    title: 'toeic',
    thumbnail: 'toeic.png'
  },
  {
    title: 'scholarship',
    thumbnail: 'scholarship.png'
  },
  {
    title: 'secondPlace',
    thumbnail: 'second place.png'
  },
  // add more...
]
</script>

<style scoped>
.github-projects {
  &> :is(h3, h4) {
    flex-basis: 100%;
    text-transform: uppercase;
  }

  & h4 {
    color: var(--color-gray-400);
    font-size: var(--text-sm);
    margin: 10px 0 15px;
  }
}

.github-projects h3 {
  margin-bottom: 1.125rem;
}

.github-projects,
.github-repositories {
  flex-wrap: wrap;
}

.github-repositories-scroll {
  display: flex;
  gap: 1rem;
  overflow-x: auto;
  padding-bottom: 1rem;
  scroll-snap-type: x mandatory;
}

.project-card {
  flex: 0 0 480px;
  /* 卡片寬度加大 */
  max-width: 480px;
  display: flex;
  flex-direction: column;
  align-items: center;
  background: #fff;
  border-radius: 12px;
  box-shadow: 0 1px 6px 0 rgba(0, 0, 0, 0.03);
  scroll-snap-align: start;
  padding: 1rem;
}

.project-card__image {
  width: 100%;
  max-width: 440px;
  height: 247.5px; /* 16:9 比例，440 / 16 * 9 = 247.5 */
  object-fit: cover;
  border-radius: 12px;
  display: block;
  margin-left: auto;
  margin-right: auto;
  background: #f5f5f5;
}

/* 只針對 h5 內的數字 */
h5 {
  font-family: "Noto Sans TC", Arial, "Microsoft JhengHei", sans-serif;
  font-variant-numeric: tabular-nums; /* 讓數字寬度一致 */
}

.number {
  font-family: Arial, "Noto Sans", "Microsoft JhengHei", sans-serif;
  font-weight: bold;
  font-size: 1em;
  letter-spacing: 0.02em;
}

@media (max-width: 600px) {
  .project-card {
    flex: 0 0 90vw;
    max-width: 95vw;
  }
  .project-card__image {
    max-width: 90vw;
    height: calc(90vw * 9 / 16); /* 16:9 比例 */
  }
}
</style>
