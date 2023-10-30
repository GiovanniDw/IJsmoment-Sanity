<!-- eslint-disable vue/no-parsing-error -->
<!-- eslint-disable vue/no-parsing-error -->
<script setup>
const props = defineProps({
  id: String,
  type: String,
  name: String,
  placeholder: String,
  class: String,
  label: String
})

import { useUserStore } from '@/stores/user.js'

const user = useUserStore()

const { email } = storeToRefs(user)

const { setEmail } = user
</script>
<template>
  <template v-if="type === 'textarea'">
    <label v-if="label" :for="id">
      {{ label }}
    </label>
    <textarea
      :id="id"
      :type="type"
      :name="name"
      :placeholder="placeholder"
      :class="class"
      @input="(event) => (text = event.target.value)"
    />
  </template>
  <template v-if="type === 'button'">
    <button
      class="btn primary"
      :id="id"
      :type="type"
      :name="name"
      :placeholder="placeholder"
      :class="class"
      @input="(event) => (text = event.target.value)"
      value="placeholder"
    >
      {{ placeholder }}
    </button>
  </template>
  <template v-else-if="type === 'email'">
    <div class="input-icon">
      <input
        class="email"
        :id="id"
        :type="type"
        :name="name"
        v-model="email"
        @input="setEmail(event.target.value)"
        :placeholder="placeholder"
        :class="class"
      />
      <label class="icon material-symbols-rounded" v-if="label" :for="id">email</label>
    </div>
  </template>
  <template v-else-if="type === 'tel'">
    <div class="input-icon">
      <input
        class="tel"
        :id="id"
        :type="type"
        :name="name"
        v-model="tel"
        @input="setEmail(event.target.value)"
        :placeholder="placeholder"
        :class="class"
      />
      <label class="icon material-symbols-rounded" v-if="label" :for="id">call</label>
    </div>
  </template>
  <template v-else-if="type !== 'textarea'">
    <label v-if="label" :for="id">
      {{ label }}
    </label>
    <input :id="id" :type="type" :name="name" :placeholder="placeholder" :class="class" />
  </template>
</template>

<style lang="scss" scoped>
input {
  padding: .25rem;
}

textarea {
  min-width: 100%;
  max-width: 100%;
  min-height: 10em;
  border-radius: var(--border-radius-small);
  appearance: none;
  border: 0.1em solid var(--color-black);
  resize: none;
  padding: .5em;
}

.input-icon {
  display: flex;
  align-items: center;
  label.icon {
    display: inline;
    color: var(--color-black);
    position: absolute;
    padding: 0.5em;
    margin-bottom: 0;
  }
  input {
    padding-left: 2.7em;
  display: inline-block;
  }
}

input[type='email'],
input[type='tel'] {
  padding-left: 2.7em;
  display: inline-block;
}




label {
  font-weight: bold;
  margin-bottom: 0.5em;
  // display: block;
}

input[type='email'],
input[type='text'],
input[type='tel'] {
  border-radius: var(--border-radius-small);
  border: 0.1em solid var(--border-color);
  color: var(--color-black);
  width: 100%;
  font-size: 1rem;
}

input[type='textarea'] {
  min-height: 10em;
  width: 100%;
  border-radius: var(--border-radius-small);

  vertical-align: top;
  text-align: start;
}

input[type='email'],
input[type='text'],
input[type='textarea'] {
  cursor: text;
  &:active {
    outline: 0.1em solid var(--border-color-active);
  }

  &:focus,
  &:focus-visible {
    outline: 0.1em solid var(--border-color-active);
  }
}
</style>
