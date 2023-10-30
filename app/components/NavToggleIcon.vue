<script setup>
defineProps({
  open: Boolean
})
</script>

<template>
  <button title="nav-toggle-button" class="nav-toggle" :class="{ open: open }">
    <span class="nav-toggle-icon" :class="{ open: open }" />
  </button>
</template>

<style lang="scss" scoped>
button.nav-toggle {
  --m-icon: 0.15em;

  text-decoration: none;
  appearance: none;
  border: 0;
  background: 0;
  padding: 0;
  // margin: auto;
  display: flex;
  position: relative;
  // justify-content: center;
  // align-content: center;
  // align-items: center;
  // justify-items: center;
  // font-size: 16px;
  transition-duration: 500ms;
  height: calc(var(--m-icon) * 10);
  width: calc(var(--m-icon) * 10);
  // transform: translateY($m-icon * 4);
  cursor: pointer;

  &.open {
    .nav-toggle-icon {
      transition: all 100ms 300ms ease;
      background: transparent;
      &:after,
      &:before {
        transition:
          all 300ms 50ms ease,
          transform 300ms 350ms ease;
        left: 0;
      }
      &:before {
        top: 0;
        transform: rotate(45deg);
      }
      &:after {
        top: 0;
        transform: rotate(-45deg);
      }
    }
  }

  .nav-toggle-icon {
    align-self: center;
    width: calc(var(--m-icon) * 10);
    height: calc(var(--m-icon) * 1);
    border-radius: calc(var(--m-icon) * 10);
    background-color: #000;
    // position: relative;
    transition: all 100ms 300ms ease;
    // transform: translateY($m-icon * 4);
    border-radius: var(--m-icon);
    // display: block;
    &:before,
    &:after {
      left: 0;
      right: 0;
      display: block;
      border-radius: calc(var(--m-icon) * 2);
      transition:
        all 300ms 350ms ease,
        transform 300ms 50ms ease;
      position: absolute;
      background: #000;
      width: calc(var(--m-icon) * 10);
      height: calc(var(--m-icon) * 1);
      content: '';
    }
    &:before {
      top: calc(var(--m-icon) * -4);
    }

    &:after {
      top: calc(var(--m-icon) * 4.4);
    }
  }
}

button.nav-toggle {
}
</style>
