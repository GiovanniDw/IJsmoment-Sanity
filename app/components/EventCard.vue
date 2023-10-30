<script setup>
const props = defineProps({ event: Object, slug: String })
</script>

<template>
  <NuxtLink :to="'/' + slug" v-editable="event" class="event-card">
    <div class="img-container">
      <img
        v-if="event.image?.filename"
        :src="getUrl(event.image.filename) + '/m/'"
        :alt="event.image.alt"
      />
    </div>
    <div class="content">
      <h3>{{ event.title }}</h3>
    </div>
  </NuxtLink>
</template>

<style scoped lang="scss">
.event-card {
  border-radius: 1em;
  overflow: hidden;
}

.img-container {
}

img {
  object-fit: cover;
  aspect-ratio: 3 / 2;
  width: 100%;
  height: auto;
}

.content {
  padding: 1rem;
  background-color: var(--color-background-alt);
  border-radius: 0 0 1em 1em;
}

h3 {
  font-size: var(--step--2);
}
</style>
