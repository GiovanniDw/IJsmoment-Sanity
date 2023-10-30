<script setup>
defineProps({ service: Object, slug: String })
</script>

<template>
  <NuxtLink :to="'/' + slug" v-editable="service" class="service-card">
    <img
      v-if="service.image?.filename"
      :src="getUrl(service.image.filename) + '/m/600x0'"
      :alt="service.image.alt"
      class=""
    />
    <div class="content">
      <h3 class="">{{ service.title }}</h3>
      <button class="btn">Meer Info</button>
    </div>
  </NuxtLink>
</template>

<style scoped lang="scss">
.img-container {
}

img {
  object-fit: cover;
  border-radius: 1rem;
  aspect-ratio: 4 / 3;
  width: 100%;
  height: auto;
}

.service-card {
  position: relative;
}

.content {
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
  padding: 1em;
  h3 {
    top: 0;
    text-align: center;
    position: relative;
    color: var(--color-text-inverse);
    filter: drop-shadow(0 0 0.5rem rgba(0, 0, 0, 0.6));
  }
}
.btn {
  background-color: var(--color-background);
  font-size: 1rem;
  padding: 0.5rem 0.75rem;
}
</style>
