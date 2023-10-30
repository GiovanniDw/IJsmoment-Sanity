<script setup>
const { y } = useWindowScroll()

const mobileNavOpen = ref(false)
const toggleMobileNav = useToggle(mobileNavOpen)
const mobile = breakpoints().smaller('tablet')
const largerThanMobile = breakpoints().greater('tablet')

const storyblokApi = useStoryblokApi()
const { data } = await storyblokApi.get('cdn/stories/config', {
  version: 'draft',
  resolve_links: 'url'
})

const headerMenu = ref(null)
headerMenu.value = data.story.content.header_menu

const route = useRoute()

const currentRoute = computed(() => route.params.slug)

watch(currentRoute, (newRoute) => {
  console.log(newRoute)
  console.log(currentRoute.value)

  if (newRoute === currentRoute.value) {
    setTimeout(() => {
      mobileNavOpen.value = false
    }, 500)
  }
})

watch(largerThanMobile, (isLargerThanMobile) => {
  if (isLargerThanMobile === true) {
    mobileNavOpen.value = false
  }
})

useHead({
  bodyAttrs: {
    class: computed(() => {
      if (mobileNavOpen.value) return 'menu-is-open'
      return ''
    })
  }
})
</script>

<template>
  <header
    :class="{
      scrolled: y > 10,
      'mobile-header': mobile,
      'mobile-header-open': mobileNavOpen && largerThanMobile === false
    }"
  >
    <div class="header-container">
      <div class="header-begin">
        <NuxtLink title="link to home" class="header-brand" to="/">
          <img src="~/assets/logo.svg" class="logo" alt="Logo Image" width="130px" height="50px" />
        </NuxtLink>
        <div class="header-top-right" v-show="mobile">
          <NuxtLink class="btn primary button">
            Boek ons!
            <!-- <span class="icon material-symbols-rounded">chevron_right</span> -->
          </NuxtLink>
          <Transition>
            <NavToggleIcon
              class="nav-toggle"
              title="nav-toggle-button"
              @click="toggleMobileNav()"
              :open="mobileNavOpen"
              :class="{ open: mobileNavOpen }"
            />
          </Transition>
        </div>
      </div>
      <Transition name="nav-menu">
        <div
          :class="{
            'header-right': largerThanMobile,
            'header-menu-open': mobileNavOpen
          }"
          class="header-menu"
          v-if="largerThanMobile === true || mobileNavOpen"
        >
          <nav
            role="navigation"
            v-if="headerMenu"
            class="header-start"
            :class="{ open: mobileNavOpen }"
          >
            <template v-for="item in headerMenu">
              <NuxtLink
                class="router-link"
                v-if="item.link.linktype === 'story'"
                :to="`/${item.link.cached_url === 'home' ? '' : item.link.cached_url}`"
                :key="item.link.id"
              >
                {{ item.link.story.name }}
              </NuxtLink>
              <NuxtLink
                v-else
                class="router-link"
                :to="`/${item.link.cached_url}`"
                :key="item._uid"
                target="_blank"
                :external="true"
                rel="noopener noreferrer"
              >
                {{ item.link.cached_url }}
                <span class="icon material-symbols-rounded">open_in_new</span>
              </NuxtLink>
            </template>
          </nav>
          <div class="header-end">
            <button role="button" class="btn primary button">
              Boek ons
              <!-- <span class="icon material-symbols-rounded">chevron_right</span> -->
            </button>
          </div>
        </div>
      </Transition>
    </div>
  </header>
</template>

<style>
.menu-is-open {
  overflow: hidden;
}
</style>

<style scoped lang="scss">
.router-link {
  text-decoration: none;
  text-wrap: default;
  border-bottom: 0.125em solid var(--color-background);
}
nav.header-start:deep(.router-link-active) {
  color: var(--color-text);
  font-weight: 400;
  border-bottom: 0.125em solid var(--color-primary);
}
.header-brand {
  opacity: 1;
  border-radius: 1em;
  // overflow: visible;
  position: relative;

  top: 0;
  // left: 0;
  // background: var(--color-background);
  // margin: 0 -1em -0.6em;
  cursor: pointer;

  .logo {
    // transform: scale(1.001) translate(1em, 0.5em);
    position: relative;
    top: 1em;
    padding: 0 1em 0.5em;
    // margin: 0 -1em -0.6em;
    background: var(--color-background);
    border-radius: 1em;
    min-width: 140px;
  }
}
header {
  position: sticky;
  width: 100%;
  display: flex;
  top: 0;
  left: 0;
  right: 0;
  // padding: 0 1em;
  // max-height: 50px;
  z-index: var(--z-index-header);
  // background: var(--color-background);
  // transition: all 300ms ease;
  // margin-bottom: 1.5rem;
  // height: auto;
  // transition: height 300ms ease-in-out;
  flex-direction: column;
  transition: filter 200ms ease-in-out;

  &.scrolled {
    // box-shadow: var(--box-shadow);
    filter: drop-shadow(0 10px 0.5rem rgba(0, 0, 0, 0.1));
  }

  .header-container {
    width: 100%;
    justify-content: space-between;
    padding: 0;
    background: initial;

    .header-begin {
      position: sticky;
      width: 100%;
      display: flex;
      padding: 0 1em;
      justify-content: space-between;
      background: var(--color-background);
      z-index: var(--z-index-header);
    }
    .header-top-right {
      display: flex;
      gap: 1em;
      align-items: center;
    }
    nav.header-start {
      flex-direction: column;
      opacity: 1;
      position: relative;
      // transition: opacity 300ms ease-in-out;
      // transition-delay: 500ms;
    }

    .header-end {
      // padding: 1em;
      // margin-bottom: 1em;
      display: flex;
      justify-content: space-around;
      justify-items: baseline;
      text-align: center;
      position: relative;
      opacity: 1;
      padding-right: 1em;
    }
  }

  &.mobile-header .header-container {
    position: sticky;
    display: flex;
    justify-content: space-between;
    width: 100%;

    // height: auto;
    // max-height: 50px;
    // transition: all 300ms ease-in-out;
    // transition-delay: 0ms;
    flex-direction: column;

    .header-menu {
      //was header Dropdown

      z-index: var(--z-index-mobile-header-menu);

      // top: 0;
      // left: 0;
      // bottom: 0;
      // right: 0;
      // min-height: 100vh;
      // max-height: 100vh;
      width: 100%;
      display: flex;
      flex-direction: column;
      justify-content: space-between;

      // height: 0;
      // overflow: hidden;
      // opacity: 0;
      background-color: var(--color-background);
      // min-height: 100vmax;
      // transition: all 100ms ease-in-out;
      // translate: 0 -100%;
      // opacity: 0;
      padding: env(safe-area-inset-bottom);
      padding: 1em;
      position: absolute;
      // height: 0;

      &.header-menu-open {
        height: 100svh;
        position: fixed;
        padding-top: 6em;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        width: 100%;
        // opacity: 1;
        // translate: 0 0;
      }
    }
  }

  &.mobile-header-open {
    // position: fixed;
    // min-height: 100vh;
    // height: 100%;
    // max-height: 100dvh;
    // display: flex;
    // flex-direction: column;
    // justify-content: space-between;
    // transition: all 300ms ease-in-out;
    // transition-delay: 500ms;
    // border: 1px solid red;

    .header-container .header-dropdown {
      // position: relative;
      // // top: 0;
      // // left: 0;
      // // bottom: 0;
      // // right: 0;
      // height: 100vh;
      // width: 100%;
      // display: flex;
      // flex-direction: column;
      // justify-content: space-around;
      // background-color: var(--color-background);
      // min-height: 100vmax;
      // transition: all 500ms ease-in-out;
    }
  }
}

.header-right {
  transition: none !important;
  transform: none !important;
}

nav.header-start {
  height: auto;
  // height: 100%;
  overflow: initial;
  display: flex;
  flex-direction: column;
  // gap: 1em;
  align-items: flex-start;
  opacity: 1;
  // height: 0;
  position: relative;
  transition: all 300ms ease-in-out;
  justify-content: center;
  position: absolute;
  // top: -1000px;
  &.open {
    // top: auto;
    // height: auto;
    // overflow: initial;
    // opacity: 1;
    transition: all 100ms ease-in-out;
  }

  &:deep(a) {
    padding: 0.92em;
    height: 100%;
  }
}
.header-container {
  display: flex;
  flex-direction: row;
}

@media (min-width: 768px) {
  header {
    // display: grid;
    // flex-direction: row;
    // justify-content: space-between;

    .header-container {
      min-width: 100%;
      display: grid;
      grid-template-columns: auto auto auto;
      max-height: 50px;
      background-color: var(--color-background);

      .header-menu {
        display: grid;
        // display: flex;
        // justify-content: space-between;
        grid-template-columns: subgrid;
        grid-column: 2 / 4;
        max-height: 50px;
        position: relative;

        .header-start {
        }
      }

      .header-begin {
        // max-width: 100%;
        justify-self: start;
        width: auto;
        max-height: auto;
        display: flex;
        justify-content: space-between;
        z-index: var(--z-index-header);
      }
      .header-top-right {
        display: flex;
        gap: 1em;
        align-items: center;
      }
      nav.header-start {
        height: auto;
        flex-direction: row;
        opacity: 1;
        position: relative;
        top: initial;
        overflow-x: scroll;
        overflow-y: hidden;
      }
      .header-end {
        // display: flex;
        // align-content: center;
        // justify-items: center;
        justify-self: end;
        justify-content: space-around;
        justify-items: center;
        align-items: center;
        opacity: 1;
        position: relative;
        // text-align: center;
      }
    }
  }
}

.nav-menu-enter-active {
  animation: move-in 0.5s;
}
.nav-menu-leave-active {
  animation: move-in 0.5s reverse;
}

.nav-menu-enter-active,
.nav-menu-leave-active {
  transition: all 0.3s ease-in-out;
  height: 100vh;
  // position: absolute;
  opacity: 1;
}

.nav-menu-enter-from,
.nav-menu-leave-to {
  opacity: 0;
  // max-height: 0vh;
  height: 0vh;
  // position: relative;
}

.nav-menu-enter-active .header-start,
.nav-menu-leave-active .header-start {
  transition: all 0.5s ease-in-out;
  transition-delay: 1s;
}

.nav-menu-enter-from .header-start,
.nav-menu-leave-to .header-start {
  // transform: translateX(1000px);
  opacity: 1;
  // transition-delay: 1s;
}
.nav-menu-enter-active .header-start {
  transition-delay: 1s;
  opacity: 0;
  // transform: translateX(0);
}

.nav-menu-enter-active .header-end,
.nav-menu-leave-active .header-end {
  transition: all 0.5s ease-in-out;
  transition-delay: 2s;
}

.nav-menu-enter-from .header-end,
.nav-menu-leave-to .header-end {
  // transform: translateX(1000px);
  opacity: 1;
  // transition-delay: 1s;
}
.nav-menu-enter-active .header-end {
  transition-delay: 1s;
  opacity: 0;
  // transform: translateX(0);
}

@keyframes move-in {
  0% {
    // transform: scale(0);
    translate: 0 -100%;
  }
  50% {
    // transform: scale(1.25);
  }
  100% {
    // transform: scale(1);
    translate: 0 0;
  }
}
</style>
