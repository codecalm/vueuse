<template>
  <header v-if="showHero" class="home-hero">
    <!-- <figure v-if="$frontmatter.heroImage" class="figure">
      <img class="image" :src="$withBase($frontmatter.heroImage)" :alt="$frontmatter.heroAlt">
    </figure>

    <h1 v-if="hasHeroText" class="title">
      {{ heroText }}
    </h1>
    <p v-if="hasTagline" class="description">
      {{ tagline }}
    </p> -->

    <p align="center">
      <a href="https://github.com/antfu/vueuse">
        <img v-if="isDark" src="/logo-vertical-dark.png" alt="VueUse - Collection of essential Vue Composition Utilities" height="300">
        <img v-else src="/logo-vertical.png" alt="VueUse - Collection of essential Vue Composition Utilities" height="300">
      </a>
      <br>
    </p>
    <div class="description">
      Collection of essential Vue Composition Utilities
    </div>

    <NavLink
      v-if="hasAction"
      :item="{ link: data.actionLink, text: data.actionText }"
      class="action mx-2"
    />

    <NavLink
      v-if="hasAltAction"
      :item="{ link: data.altActionLink, text: data.altActionText }"
      class="action alt mx-2"
    />
  </header>
</template>

<script setup lang="ts">
import { computed } from 'vue'
import { useSiteDataByRoute, useFrontmatter } from 'vitepress'
import { isDark } from '../composables/darkmode'
import NavLink from './NavLink.vue'

const site = useSiteDataByRoute()
const data = useFrontmatter()

const showHero = computed(() => {
  return data.value.heroImage
    || hasHeroText.value
    || hasTagline.value
    || hasAction.value
})

const hasHeroText = computed(() => data.value.heroText !== null)
const heroText = computed(() => data.value.heroText || site.value.title)

const hasTagline = computed(() => data.value.tagline !== null)
const tagline = computed(() => data.value.tagline || site.value.description)

const hasAction = computed(() => data.value.actionLink && data.value.actionText)
const hasAltAction = computed(() => data.value.altActionLink && data.value.altActionText)
</script>

<style scoped>
.home-hero {
  margin: 2.5rem 0 2.75rem;
  padding: 0 1.5rem;
  text-align: center;
}

@media (min-width: 420px) {
  .home-hero {
    margin: 3.5rem 0;
  }
}

@media (min-width: 720px) {
  .home-hero {
    margin: 4rem 0 4.25rem;
  }
}

.figure {
  padding: 0 1.5rem;
}

.image {
  display: block;
  margin: 0 auto;
  width: auto;
  max-width: 100%;
  max-height: 280px;
}

.title {
  margin-top: 1.5rem;
  font-size: 2rem;
}

@media (min-width: 420px) {
  .title {
    font-size: 3rem;
  }
}

@media (min-width: 720px) {
  .title {
    margin-top: 2rem;
  }
}

.description {
  margin: 0;
  line-height: 1.3;
  font-size: 1.2rem;
  color: var(--c-text-light);
}

.action {
  margin-top: 1.5rem;
  display: inline-block;
}

.action.alt {
  margin-left: 1.5rem;
}

@media (min-width: 420px) {
  .action {
    margin-top: 2rem;
    display: inline-block;
  }
}

.action :deep(.item) {
  display: inline-block;
  border-radius: 6px;
  padding: 0 18px;
  line-height: 40px;
  font-size: 1.1rem;
  font-weight: 500;
  border: 0;
  color: #ffffff;
  background-color: var(--c-brand);
  transition: background-color 0.1s ease;
}

.action :deep(.item:hover) {
  text-decoration: none;
  color: #ffffff;
  background-color: var(--c-brand-light);
}

.action.alt :deep(.item) {
  background-color: #476582;
}

.action.alt :deep(.item:hover) {
  background-color: #304a64;
}
</style>
