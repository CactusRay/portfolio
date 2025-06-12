<template>
  <header class="header">
    <div class="nav">
      <router-link to="/">
        <h3>{{ $t('home') }}</h3>
      </router-link>
      <nav class="navbar">
        <ul class="navbar-menu">
          <!-- <li class="navbar-menu__item">
            <router-link class="navbar-menu__link" to="/articles">
              {{ $t('articles') }}
            </router-link>
          </li> -->
          <li class="navbar-menu__item">
            <router-link class="navbar-menu__link" to="/about-me">{{ $t('skills') }}</router-link>
          </li>
          <!-- <li class="navbar-menu__item">
            <router-link class="navbar-menu__link" to="/now">
              /now
            </router-link>
          </li> -->
          <li class="navbar-menu__item no-effect">
            <HamburgerMenu aria-controls="mobile-menu" @toggle="toggleMenu(true)" />
          </li>
          <li class="navbar-menu__item no-effect">
            <ThemeSwitcher variant="transform" />
          </li>
          <!-- 地球語言切換器 -->
          <li class="navbar-menu__item no-effect">
            <button class="lang-switcher globe-btn" @click="toggleLocale" :aria-label="$i18n.locale === 'zh' ? 'Switch to English' : '切換為中文'">
              <svg xmlns="http://www.w3.org/2000/svg" width="32" height="32" fill="#3bb3f6" viewBox="0 0 256 256">
                <path d="M128,24h0A104,104,0,1,0,232,128,104.12,104.12,0,0,0,128,24Zm88,104a87.61,87.61,0,0,1-3.33,24H174.16a157.44,157.44,0,0,0,0-48h38.51A87.61,87.61,0,0,1,216,128ZM102,168H154a115.11,115.11,0,0,1-26,45A115.27,115.27,0,0,1,102,168Zm-3.9-16a140.84,140.84,0,0,1,0-48h59.88a140.84,140.84,0,0,1,0,48ZM40,128a87.61,87.61,0,0,1,3.33-24H81.84a157.44,157.44,0,0,0,0,48H43.33A87.61,87.61,0,0,1,40,128ZM154,88H102a115.11,115.11,0,0,1,26-45A115.27,115.27,0,0,1,154,88Zm52.33,0H170.71a135.28,135.28,0,0,0-22.3-45.6A88.29,88.29,0,0,1,206.37,88ZM107.59,42.4A135.28,135.28,0,0,0,85.29,88H49.63A88.29,88.29,0,0,1,107.59,42.4ZM49.63,168H85.29a135.28,135.28,0,0,0,22.3,45.6A88.29,88.29,0,0,1,49.63,168Zm98.78,45.6a135.28,135.28,0,0,0,22.3-45.6h35.66A88.29,88.29,0,0,1,148.41,213.6Z"></path>
              </svg>
            </button>
          </li>
        </ul>
      </nav>
    </div>
    <MobileNavbar @close="toggleMenu(false)">
      <li class="navbar-menu__item">
        <router-link class="navbar-menu__link" to="/articles">
          {{ $t('articles') }}
        </router-link>
      </li>
      <li class="navbar-menu__item">
        <router-link class="navbar-menu__link" to="/about-me">{{ $t('about') }}</router-link>
      </li>
      <li class="navbar-menu__item">
        <router-link class="navbar-menu__link" to="/now"> /now </router-link>
      </li>
    </MobileNavbar>
  </header>
</template>

<script setup>
defineOptions({ name: 'AppNavbar' });

const toggleMenu = (open) => {
  const button = document.querySelector('.hamburger-menu')
  const menu = document.querySelector('.mobile-navbar')

  if (open) {
    button.classList.add('hamburger-menu--active')
    menu.classList.add('mobile-navbar--opened')
    button.setAttribute('aria-expanded', true)
  } else {
    menu.classList.remove('mobile-navbar--opened')
    button.classList.remove('hamburger-menu--active')
    button.setAttribute('aria-expanded', false)
  }
}

// 語言切換
import { useI18n } from 'vue-i18n'
const { locale } = useI18n()
function toggleLocale() {
  locale.value = locale.value === 'zh' ? 'en' : 'zh'
}
</script>

<style scoped>
.header {
  position: sticky;
  top: 0;
  width: 100%;
  font-family: var(--font-title);
  z-index: var(--z-base);
  border: 1px solid hsl(214deg 9% 25% / 20%);

  & .nav {
    display: flex;
    align-items: center;
    justify-content: space-between;
    min-height: 60px;
    width: calc(100% - 2rem);
    max-width: 1110px;
    margin-inline: auto;
    padding-inline: 2rem;
    border-end-start-radius: 1rem;
    border-end-end-radius: 1rem;
  }

  & a {
    color: var(--text-color-default);
    transition: font-weight 200ms ease-out;
  }

  & ul {
    list-style-type: none;
  }
}

.navbar {
  padding: 0.3rem;
}

.navbar-menu {
  display: flex;
  align-items: center;
}

.navbar-menu__link {
  letter-spacing: 1.2px;
  outline-color: transparent;

  &:focus-visible {
    outline: 2px dashed var(--color-primary);
    outline-offset: 10px;
  }
}

.navbar-menu .navbar-menu__item {
  transition: opacity 400ms ease-out;
  position: relative;
  z-index: var(--z-base);
  padding: 2px 10px;

  &:not(.no-effect)::before {
    content: '';
    position: absolute;
    z-index: var(--z-hide);
    top: 15px;
    bottom: 0;
    left: 0;
    background: radial-gradient(circle at bottom,
        rgb(26 188 209 / 60.3%) 5%,
        rgb(0 0 0 / 0%) 60%);
    width: 100%;
    height: 100%;
    transition: transform 0.2s ease-out;
    transform: scale(0);
    transform-origin: bottom;
  }

  &:not(.no-effect):hover::before {
    transform: scale(100%);
  }

  &:hover .navbar-menu__link {
    font-weight: var(--fw-normal);
    cursor: pointer;
    text-decoration: none;
  }
}

.navbar-menu .navbar-menu__item+.navbar-menu__item {
  margin-inline-start: 30px;
}

.navbar-menu:has(:hover) .navbar-menu__item:not(:hover) {
  opacity: 0.7;
}

body[data-theme='light'] {
  .header {
    background-color: transparent;
  }

  .nav {
    background-color: hsl(216deg 9% 83% / 30%);
  }
}

@supports (-webkit-backdrop-filter: none) or (backdrop-filter: none) {
  .nav {
    background-color: hsl(216deg 8.77% 11.18% / 30%);
    backdrop-filter: blur(4px);
  }
}

@media screen and (min-width: 48em) {
  .hamburger-menu {
    display: none;
  }
}

@media (--vw-md) {
  .header {
    font-size: var(--text-base);

    & .nav {
      padding: 0;
    }
  }

  .navbar-menu {
    & .navbar-menu__item:has(a) {
      display: none;
    }
  }
}

@media (--vw-sm) {
  .header {
    font-size: var(--text-sm);
    line-height: 1.25rem;
  }

  .navbar-menu {
    & .navbar-menu__item+.navbar-menu__item {
      margin-inline-start: 1.25rem;
    }
  }
}

.lang-switcher {
  margin-left: 0.5rem;
  padding: 0.25em 0.5em;
  border-radius: 6px;
  border: 1px solid #ccc;
  background: #fff;
  font-size: 1em;
}

.lang-switcher.globe-btn {
  background: none;
  border: none;
  padding: 0.25em;
  cursor: pointer;
  display: flex;
  align-items: center;
  transition: background 0.2s;
  margin-left: -10px; /* 靠近左邊，數值可依實際需求微調 */
}
.lang-switcher.globe-btn:hover {
  background: #eaf6fb;
  border-radius: 50%;
}
</style>
