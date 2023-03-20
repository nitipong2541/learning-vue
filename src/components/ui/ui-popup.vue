<template>
  <Transition name="fade">
    <div
      v-show="open"
      class="fixed top-0 left-0 w-full h-full overflow-x-hidden overflow-y-auto bg-black opacity-80 z-1 justify-center flex"
    >
      <Transition name="drop-in">
        <div v-show="open" class="w-100 max-w-150 m-8">
          <div
            class="relative bg-white border-1 border-solid border-black bg-clip-padding rounded-md p-4"
          >
            <slot></slot>
            <div class="justify-center flex m-2">
              <ui-button type="button" @click="close">close</ui-button>
            </div>
          </div>
        </div></Transition
      >
    </div></Transition
  >
</template>

<script>
import { onMounted, onUnmounted } from "vue";
export default {
  props: {
    open: {
      type: Boolean,
      required: true,
    },
  },
  setup(_, { emit }) {
    const close = () => {
      emit("close");
    };

    const handleKeyup = (event) => {
      if (event.keyCode === 27) {
        close();
      }
    };

    onMounted(() => document.addEventListener("keyup", handleKeyup));
    onUnmounted(() => document.removeEventListener("keyup", handleKeyup));

    return { close };
  },
};
</script>

<style>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
.drop-in-enter-active,
.drop-in-leave-active {
  transition: all 0.3s ease-out;
}

.drop-in-enter-from,
.drop-in-leave-to {
  opacity: 0;
  transform: translate(0, -50px);
}
</style>
