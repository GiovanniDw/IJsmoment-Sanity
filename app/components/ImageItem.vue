<script setup>
defineProps({
  image: Object
})
</script>

<template>
  <img :src="image.filename" alt="" />
</template>

<style lang="scss" scoped>
img {
  object-fit: cover;
  object-position: 50% 50%;
  // vertical-align: bottom;
  max-height: 100%;
  // height: auto;
  min-width: 100%;
  // transition: all 0.2ms ease-in-out;
}
</style>
