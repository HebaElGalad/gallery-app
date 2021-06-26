<template functional>
  <div class="Spinner" :class="[data.class, data.staticClass]"></div>
</template>

<script>
export default {
  name: 'Spinner',
};
</script>

<style lang="postcss" scoped>
.Spinner {
  display: block;
  border-radius: 2em;
  border-color: transparent transparent currentColor currentColor;
  border-style: solid;
  border-width: 0.2em;
  animation: spinner-rotation 0.75s infinite;
  animation-timing-function: cubic-bezier(0.68, -0.55, 0.27, 1.55);
}

@keyframes spinner-rotation {
  to {
    transform: rotate(360deg);
  }
}
</style>
