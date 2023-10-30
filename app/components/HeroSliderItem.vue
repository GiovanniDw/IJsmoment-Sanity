<script setup>
const props = defineProps({
  slide: Object
})

const richtext = computed(() => renderRichText(props.slide.content))
</script>

<template>
  <div class="slide">
    <div class="content">
      <h1>{{ slide.title }}</h1>
      <div v-if="richtext" v-html="richtext" />
    </div>
    <div class="image">
      <img :src="slide.image.filename" alt="" />
    </div>
  </div>
</template>

<style lang="scss" scoped>
.slide {
  width: 100%;
  height: 100%;
  display: grid;
  grid-template-columns: 1fr 1fr;
  background: var(--color-background-alt);
}

div {
  .content {
    padding: 1em;
    overflow: hidden;
    height: 100%;
    width: 100%;
    z-index: 2;
  }
}

.image {
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  height: 100%;
  width: 100%;
  z-index: 1;

  img {
    object-fit: cover;
    object-position: 50% 50%;
    height: 100%;
  }
}
</style>
