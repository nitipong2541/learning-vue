<template>
  <button
    type="button"
    class="h-10 w-40 bg-blue-600 text-white rounded-xl flex gap-1 justify-center items-center"
    :title="text"
  >
    <slot name="icon1">
      <span v-if="icon1" class="icons">{{ icon1 }}</span></slot
    >
    <slot>Button</slot>
    <slot name="icon2">
      <span v-if="icon2" class="icons">{{ icon2 }}</span></slot
    >
  </button>
</template>

<script>
export default {
  props: {
    text: {
      type: String,
      default: "Button text",
    },
    icon1: {
      type: String,
    },
    icon2: {
      type: String,
    },
  },
};
</script>
