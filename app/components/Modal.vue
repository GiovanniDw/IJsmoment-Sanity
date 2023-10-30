<script setup>
const props = defineProps({
  show: Boolean
})

const modal = ref(null)

const { isOutside } = useMouseInElement(modal)

const { pressed } = useMousePressed()

const closeModal = () => {}
</script>

<template>
  <Transition name="modal">
    <div v-if="show" class="modal-mask">
      <div class="modal-wrapper" ref="modal">
        <div class="modal-container">
          <div class="modal-header">
            <slot name="header">default header</slot>
            <button
              class="icon material-symbols-rounded modal-close-button"
              @click="$emit('close')"
            >
              close
            </button>
          </div>
          <div class="modal-body">
            <slot name="content" />
          </div>
        </div>
      </div>
    </div>
  </Transition>
</template>

<style lang="scss" scoped>
.modal-mask {
  position: fixed;
  z-index: 9998;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: table;
  transition: opacity 0.3s ease;
}

.modal-wrapper {
  display: table-cell;
  vertical-align: middle;
}

.modal-container {
  border-radius: var(--border-radius-small);
  max-width: 50em;
  min-width: 5em;
  margin: 0px auto;
  padding: var(--padding-m) var(--padding-m);
  background-color: #fff;

  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
  transition: all 0.3s ease;
}

.modal-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.modal-header h3 {
  margin-top: 0;
  color: #42b983;
}

.modal-body {
  margin: 20px 0;
}

button {
  appearance: none;
  padding: 0;
  border: 0;
  border-radius: 100%;
  color: var(--color-white);
  font-weight: bold;
  background-color: var(--color-gray);
  box-shadow: var(--box-shadow);
  .modal-default-button {
    // float: right;
    border: 0px;
    background: 0;
    appearance: none;
  }
}
/*
 * The following styles are auto-applied to elements with
 * transition="modal" when their visibility is toggled
 * by Vue.js.
 *
 * You can easily play with the modal transition by editing
 * these styles.
 */

.modal-enter-from {
  opacity: 0;
}

.modal-leave-to {
  opacity: 0;
}

.modal-enter-from .modal-container,
.modal-leave-to .modal-container {
  -webkit-transform: scale(0.8);
  transform: scale(0.8);
}
</style>
