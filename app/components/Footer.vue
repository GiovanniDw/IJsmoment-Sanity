<script setup>
const storyblokApi = useStoryblokApi()
const { data } = await storyblokApi.get('cdn/stories/config', {
  version: 'draft',
  resolve_links: 'url'
})

const footerMenu = ref(null)
const footerMenuList = ref(null)
footerMenu.value = data.story.content.footer_menu
footerMenuList.value = data.story.content.footer_menu_list
</script>

<template>
  <footer>
    <NuxtLink class="brand" to="/">
      <img src="~/assets/logo.svg" alt="" />
    </NuxtLink>
    <nav v-if="footerMenu">
      <template v-for="(blok, index) in footerMenuList" :key="index">
        <div>
          <NuxtLink
            v-if="blok.link.linktype === 'story'"
            :to="`/${blok.link.cached_url === 'home' ? '' : blok.link.cached_url}`"
            :key="blok.link.id"
            class="link-title"
          >
            {{ blok.link.story.name }}
          </NuxtLink>
          <NuxtLink v-else :item="blok" :to="`/${blok.link.cached_url}`" :key="blok._uid">
            {{ blok.link.story.name }}
            <span class="icon material-symbols-rounded">open_in_new</span>
          </NuxtLink>
          <template v-for="blok in blok.links">
            <NuxtLink
              v-if="blok.link.linktype === 'story'"
              :to="`/${blok.link.cached_url === 'home' ? '' : blok.link.cached_url}`"
              :key="blok.link.id"
            >
              {{ blok.link.story.name }}
            </NuxtLink>
            <NuxtLink v-else :item="blok" :to="`/${blok.link.cached_url}`" :key="blok._uid">
              {{ blok.link.story.name }}
              <span class="icon material-symbols-rounded">open_in_new</span>
            </NuxtLink>
          </template>
        </div>
      </template>
    </nav>
  </footer>
</template>

<style scoped lang="scss">
.link-title {
  // font-size: 1.2em;
  font-weight: 500;
}
footer {
  background: var(--color-background-alt);
  padding: 1em;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: flex-start;
  gap: 0.75rem;
  bottom: 0;
  width: 100%;
  overscroll-behavior: contain;
  touch-action: none;
  z-index: var(--z-index-footer);

  .brand {
    // height: 1.5em;
    font-size: 1.5em;
    padding: var(--padding-s);

    max-width: 150px;
  }

  nav {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr 1fr;
    gap: 1rem;

    div {
      display: flex;
      flex-direction: column;
    }

    a {
      text-decoration: none;
      display: inline-flex;
      align-items: center;
      color: var(--color-black);
      padding: var(--padding-s);
      font-size: 1em;
      &:hover {
        opacity: 0.8;
      }
    }
    @media (max-width: 650px) {
      flex-wrap: wrap;

      a:first-child {
        // display: none;
        width: 100%;
        align-self: stretch;
      }
    }
  }
}
</style>
