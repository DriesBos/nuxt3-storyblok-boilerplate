<template>
  <header class="header">
    <div class="header-Logo">
      <NuxtLink to="/">
        <h1>Nuxt Storyblok Boilerplate</h1>
      </NuxtLink>
    </div>
    <div class="header-Nav">
      <nav v-if="headerMenu">
        <ul>
          <li
            v-for="blok in headerMenu"
            class="cursorInteract"
            :key="blok._uid"
          >
            <NuxtLink :to="blok.link.cached_url"
              >{{ blok.link.story.name }}
            </NuxtLink>
          </li>
        </ul>
      </nav>
    </div>
  </header>
</template>

<script setup>
const storyblokApi = useStoryblokApi();
const { data } = await storyblokApi.get('cdn/stories/config', {
  version: 'draft',
  resolve_links: 'url',
});

const headerMenu = ref(null);
headerMenu.value = data.story.content.header_menu;
</script>

<style lang="sass" scoped>
.header
  display: flex
  justify-content: space-between
  &-Logo
    padding: 1em
  &-Nav
    ul
      display: flex
      li
        padding: 1em
  a
    text-decoration: none
    &:hover
      text-decoration: underline
</style>
