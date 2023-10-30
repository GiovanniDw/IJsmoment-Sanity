<script setup>
const props = defineProps({ blok: Object })

const heroClasses = computed(() => {
  return props.blok.layout === 'constrained' ? 'container mx-auto' : ''
})
</script>

<template>
  <nav id="topNav" class="navbar navbar-default navbar-fixed-top">
    <div class="container-fluid">
      <div class="navbar-header">
        <button
          type="button"
          class="navbar-toggle collapsed"
          data-toggle="collapse"
          data-target="#bs-navbar"
        >
          <span class="sr-only">Toggle navigation</span>
          <span class="icon-bar"></span>
          <span class="icon-bar"></span>
          <span class="icon-bar"></span>
        </button>
        <a class="navbar-brand page-scroll" href="#first">
          <i class="ion-ios-analytics-outline"></i> Landing Zero
        </a>
      </div>
      <div class="navbar-collapse collapse" id="bs-navbar">
        <ul class="nav navbar-nav">
          <li>
            <a class="page-scroll" href="#one">Intro</a>
          </li>
          <li>
            <a class="page-scroll" href="#two">Highlights</a>
          </li>
          <li>
            <a class="page-scroll" href="#three">Gallery</a>
          </li>
          <li>
            <a class="page-scroll" href="#four">Features</a>
          </li>
          <li>
            <a class="page-scroll" href="#last">Contact</a>
          </li>
        </ul>
        <div class="nav navbar-nav navbar-right">
          <a
            class="page-scroll"
            data-toggle="modal"
            title="A free Bootstrap video landing theme"
            href="#aboutModal"
          >
            About
          </a>
        </div>
      </div>
    </div>
  </nav>
</template>

<style lang="scss" scoped>
.navbar-default {
  border-color: rgba(35, 35, 35, 0.05);
  font-family: 'Questrial', 'Helvetica Neue', Arial, sans-serif;
  background-color: #222;
  -webkit-transition: all 0.4s;
  -moz-transition: all 0.4s;
  transition: all 0.4s;
}

.navbar-header > .navbar-brand {
  font-family: 'Questrial', 'Helvetica Neue', Arial, sans-serif;
  color: #9c27b0;
  padding: 15px;
  -webkit-transition: padding 0.2s ease-in;
  -moz-transition: padding 0.2s ease-in;
  transition: padding 0.2s ease-in;
}

.navbar-header > .navbar-brand:hover,
.navbar-header > .navbar-brand:focus {
  color: #8b27b0;
}

.navbar-default .navbar-toggle:focus,
.navbar-default .navbar-toggle:hover {
  background-color: #181818;
}
.navbar-default .navbar-toggle,
.navbar-default .navbar-collapse {
  border-color: transparent;
}

.navbar-default .nav > li > a,
.navbar-default .nav > li > a:focus {
  text-transform: uppercase;
  font-size: 13px;
  font-weight: 700;
  color: #eee;
}

.navbar-default .nav > li > a:hover,
.navbar-default .nav > li > a:focus:hover {
  color: #9c27b0;
}

.navbar-default .nav > li.active > a,
.navbar-default .nav > li.active > a:focus {
  color: #9c27b0 !important;
  background-color: transparent;
}

.navbar-default .nav > li.active > a:hover,
.navbar-default .nav > li.active > a:focus:hover {
  background-color: transparent;
}

@media (min-width: 768px) {
  .navbar-default {
    border-color: transparent;
    background-color: transparent;
    min-height: 60px;
  }

  .navbar-header > .navbar-brand {
    color: rgba(255, 255, 255, 0.7);
    padding: 19px;
  }

  .navbar-default .navbar-header .navbar-brand:hover,
  .navbar-default .navbar-header .navbar-brand:focus {
    color: #f4f4f4;
  }

  .navbar-default .nav > li > a,
  .navbar-default .nav > li > a:focus {
    color: rgba(255, 255, 255, 0.8);
    padding: 20px;
    letter-spacing: 1.1px;
    text-shadow: 1px 1px 1px rgba(60, 60, 60, 0.7);
  }

  .navbar-default .nav > li > a:hover,
  .navbar-default .nav > li > a:focus:hover {
    color: #fefefe;
  }

  .navbar-default.affix {
    border-color: rgba(34, 34, 34, 0.05);
    background-color: #222;
  }

  .navbar-default.affix .navbar-header .navbar-brand {
    font-size: 15px;
    color: #9c27b0;
    padding: 20px;
    letter-spacing: 1px;
  }

  .navbar-default.affix .navbar-header .navbar-brand:hover,
  .navbar-default.affix .navbar-header .navbar-brand:focus {
    color: #8b27b0;
  }

  .navbar-default.affix .nav > li > a,
  .navbar-default.affix .nav > li > a:focus {
    color: #ddd;
    text-shadow: 1px 1px 1px rgba(30, 30, 30, 0.7);
  }

  .navbar-default.affix .nav > li > a:hover,
  .navbar-default.affix .nav > li > a:focus:hover {
    color: #9c27b0;
  }
}
</style>
