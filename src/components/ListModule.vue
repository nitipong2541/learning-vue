<template>
  <li>
    <div class="flex">
      <button @click="$emit('remove')" class="border-2 border-red-600">Remove</button>
      <div>
        {{ title }}
      </div>
    </div>
  </li>
</template>

<script>
export default {
  props: ["title"],
  emits: ["remove"],
};
</script>
