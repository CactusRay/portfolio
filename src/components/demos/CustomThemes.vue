<template>
  <div class="theme-control">
    <input id="warm" v-model="theme" type="radio" name="theme" value="warm" />
    <label for="warm">Warm</label>

    <!-- <input id="dark" v-model="theme" type="radio" name="theme" value="dark" />
    <label for="dark">Dark</label> -->

    <input
      id="spacegray"
      v-model="theme"
      type="radio"
      name="theme"
      value="spacegray"
    />
    <label for="spacegray">Spacegray</label>

    <div ref="body" class="preview-body">
      <div class="card">
        <h2 class="card__title">Headline</h2>
        <div class="card__content">
          <p class="card__text">
            Lorem ipsum dolor sit amet consectetur adipisicing elit. Repudiandae
            inventore neque nostrum sint rerum exercitationem possimus assumenda
            doloremque nemo? Quis.
          </p>
        </div>
        <div class="card__footer">
          <div class="call-to-action">
            <button>Read more</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      theme: 'spacegray',
      themeObject: {
        'bg-color': '#fff',
        'text-color': '#303030',
        'accent-color': '#374151',
      },
    }
  },
  watch: {
    theme() {
      this.$refs.body.style = ''
      this.setTheme(this.theme)
    },
  },
  mounted() {
    this.setTheme(this.theme)
  },
  methods: {
    setTheme(theme) {
      if (this.theme === 'custom') {
        Object.keys(this.themeObject).forEach((key) => {
          this.$refs.body.style.setProperty(`--v-${key}`, this.themeObject[key])
        })
      } else {
        this.$refs.body.setAttribute('data-v-theme', theme)
      }
    },
  },
}
</script>

<style scoped>
.theme-control {
  border: var(--border);
  border-radius: var(--radius-default);
}

.preview-body {
  --v-text-color: hsl(0deg 0% 19%);
  --v-bg-color: hsl(0deg 0% 96%);
  --v-accent-color: hsl(240deg 76% 67%);
  --v-font: var(--font-sans);

  padding: 1.2rem 2rem;
  background: var(--v-bg-color);
  color: var(--v-text-color);
  border-radius: var(--radius-default);
  margin-block-start: 10px;
}

/* [data-v-theme='dark'] {
  --v-text-color: hsl(0deg 0% 100%);
  --v-bg-color: hsl(0deg 0% 0%);
  --v-accent-color: hsl(145deg 63% 49%);
  --v-font: var(--font-mono);
} */

[data-v-theme='spacegray'] {
  --v-text-color: hsl(0deg 0% 100%);
  --v-bg-color: hsl(210deg 28% 29%);
  --v-accent-color: hsl(33deg 66% 49%);
}

[data-v-theme='warm'] {
  --v-bg-color: hsl(37deg 90% 91%);
  --v-accent-color: hsl(196deg 97% 49%);
  --v-text-color: hsl(35deg 9% 37%);
  --v-font: var(--font-serif);
}

.card {
  font-family: var(--v-font);
}

.card button {
  --v-button-padding: 8px 16px;

  padding: var(--v-button-padding);
  background-color: var(--v-accent-color);
}
</style>
