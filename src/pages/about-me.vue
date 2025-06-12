<template>
  <div class="container">
    <main id="main-content">
      <article class="about-content">
        <picture>
          <img src="@/assets/img/profile.jpg" alt="me" width="140" height="190" loading="lazy" />
        </picture>
        <h1 class="about-content__headline">{{ $t('aboutMe') }}</h1>
        <p>
          {{ $t('hi') }}
          <strong>{{ $t('jobTitle') }}</strong>，{{ $t('aboutDesc1') }}
        </p>
        <p v-html="$t('aboutDesc2')"></p>
        <br>
        <p v-html="$t('aboutDesc3')"></p>
      </article>
      <SocialMediaIcons boxed />
      <section class="work-experience-blocks rounded-block">
        <h1>{{ $t('workExperience') }}</h1><br>
        <div class="job-block">
          <h3>{{ $t('job1Title') }}</h3>
          <p>{{ $t('job1Company') }}</p>
          <ul>
            <li v-for="(item, idx) in job1List" :key="idx" v-html="item"></li>
          </ul>
        </div>
        <br>
        <div class="job-block">
          <h3>{{ $t('job2Title') }}</h3>
          <p>{{ $t('job2Company') }}</p>
          <ul>
            <li v-for="(item, idx) in job2List" :key="idx" v-html="item"></li>
          </ul>
        </div>
        <br>
        <div class="job-block">
          <h3>{{ $t('job3Title') }}</h3>
          <p>{{ $t('job3Company') }}</p>
          <ul>
            <li v-for="(item, idx) in job3List" :key="idx" v-html="item"></li>
          </ul>
        </div>
      </section>
      <br>
      <section class="skills-blocks rounded-block">
        <h1>{{ $t('skills') }}</h1>
        <br>
        <div class="skill-block">
          <h3>{{ $t('backend') }}</h3>
          <p>{{ $t('backendSkills') }}</p>
        </div>
        <div class="skill-block">
          <h3>{{ $t('frontend') }}</h3>
          <p>{{ $t('frontendSkills') }}</p>
        </div>
        <div class="skill-block">
          <h3>{{ $t('database') }}</h3>
          <p>{{ $t('databaseSkills') }}</p>
        </div>
        <div class="skill-block">
          <h3>{{ $t('versionControl') }}</h3>
          <p>{{ $t('versionControlSkills') }}</p>
        </div>
        <div class="skill-block">
          <h3>{{ $t('language') }}</h3>
          <p>{{ $t('languageSkills') }}</p>
        </div>
      </section>
    </main>
  </div>
</template>

<script setup>
import config from '../config/siteconfig.json'
import { computed } from 'vue'
import { useI18n } from 'vue-i18n'
import { useRoute } from 'vue-router'
const route = useRoute()

const { locale, messages } = useI18n()

const job1List = computed(() => messages.value[locale.value].job1List)
const job2List = computed(() => messages.value[locale.value].job2List)
const job3List = computed(() => messages.value[locale.value].job3List)

const title = 'About me • Jeferson S. Brito'
const { description } = config

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
</script>

<route lang="yaml">
meta:
  layout: default
</route>

<style lang="css" scoped>
.container {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  max-width: 800px;
  margin: 0 auto;
  padding: 3rem 1rem;
}

.work-experience-blocks {
  border: 2px solid #e0e0e0;
  border-radius: 18px;
  padding: 2rem 1.5rem;
  background: #fff;
  box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.04);
  margin-top: 2rem;
}

.work-experience-blocks h1 {
  text-align: center;
}

.work-experience-blocks ul {
  padding-left: 1.5rem;
  padding-right: 1.5rem;
  margin-bottom: 0.5rem;
}

.job-block {
  border: 1px solid #e0e0e0;
  border-radius: 12px;
  padding: 1.2rem 1rem;
  background: #fafbfc;
  margin-bottom: 1.5rem;
  box-shadow: 0 1px 6px 0 rgba(0, 0, 0, 0.03);
  transition: box-shadow 0.2s, transform 0.2s;
}

.job-block:hover {
  box-shadow: 0 8px 24px 0 rgba(0, 0, 0, 0.10);
}

.job-block p {
  opacity: 0.7;
}

.about-content {
  margin-block-end: 2rem;

  & picture {
    float: left;
    shape-outside: ellipse(50% 50%);
    margin: 0 1.125rem 0 0;
    position: relative;

    & img {
      max-width: 140px;
      clip-path: circle(70px at center);
      object-fit: cover;
    }

    &::before {
      content: '';
      position: absolute;
      display: block;
      width: 155px;
      height: 155px;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%) rotate(0deg);
      outline: 3px inset var(--color-silver);
      border-radius: 9999px;
      will-change: transform;
    }
  }

  & .about-content__headline {
    font-size: var(--text-2xl);
  }

  & p {
    font-size: var(--text-lg);
    opacity: 0.8;
    max-width: 71ch;
    margin-top: 0.50em;
  }
}

.skills-blocks {
  border: 1px solid #e0e0e0;
  border-radius: 12px;
  padding: 1.2rem 1rem;
  background: #fafbfc;
  margin-bottom: 1.5rem;
  box-shadow: 0 1px 6px 0 rgba(0, 0, 0, 0.03);
  transition: box-shadow 0.2s, transform 0.2s;
}

.skills-blocks h1 {
  text-align: center;
}

.skill-block {
  border: 1px solid #e0e0e0;
  border-radius: 12px;
  padding: 1.2rem 1rem;
  background: #fafbfc;
  margin-bottom: 1.5rem;
  box-shadow: 0 1px 6px 0 rgba(0, 0, 0, 0.03);
  transition: box-shadow 0.2s, transform 0.2s;
}

.skill-block:hover {
  box-shadow: 0 8px 24px 0 rgba(0, 0, 0, 0.10);
}

.skill-block p {
  opacity: 0.7;
  margin: 0;
}

.binary-text-svg {
  font-family: var(--font-mono);
  font-size: var(--text-xl);
  position: absolute;
  left: 282px;
  top: 387px;
  opacity: 0.3;

  & :deep(tspan) {
    --text-delay: 500ms;

    opacity: 0;
    animation: pulse-spread 3s var(--text-delay) ease-out infinite alternate;

    &:nth-child(1) {
      --text-delay: 500ms;
    }

    &:nth-child(2) {
      --text-delay: 1s;
    }

    &:nth-child(3) {
      --text-delay: 1.5s;
    }

    &:nth-child(4) {
      --text-delay: 2s;
    }

    &:nth-child(5) {
      --text-delay: 2.5s;
    }

    &:nth-child(6) {
      --text-delay: 3s;
    }
  }
}

@keyframes pulse-spread {
  0% {
    opacity: 0;
  }

  100% {
    opacity: 0.3;
  }
}

@media screen and (min-width: 26.625em) and (max-width: 48em) {
  aside {
    margin-inline-start: 40px;
    padding: 0 2.4rem 0 0;
  }
}

@media (--vw-sm) {
  aside {
    padding: 0 1rem;
  }

  .container {
    height: 100%;
  }

  .binary-text-svg {
    top: 50%;
    left: 0;
    bottom: 0;
  }
}
</style>