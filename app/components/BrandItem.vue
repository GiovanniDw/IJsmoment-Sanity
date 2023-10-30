<script setup>
const props = defineProps({ item: Object })
</script>

<template>
  <NuxtLink class="brand" :title="item.name" :target="item.url.target" :to="item.url.url">
    <img :src="item.logo.filename" alt="" />
  </NuxtLink>
</template>

<style lang="scss" scoped>
.brand {
  display: flex;
  width: 100%;
  justify-items: center;
  align-content: center;
  align-items: center;
  // min-width: 150px;
  max-width: 100px;
  max-height: 70px;
  height: 70px;
  // width: 100%;
  // overflow: hidden;
  img {
    // max-width: 100%;
    width: auto;
    max-height: 70px;
    object-fit: contain;
    object-position: 50% 50%;
  }
}
</style>
