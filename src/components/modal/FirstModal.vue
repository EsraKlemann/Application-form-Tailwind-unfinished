<template>
  <teleport to="body">
    <div @click="$emit('close')"
      class="bg-gray-500/60 fixed top-0 left-0 h-full w-full overflow-x-hidden overflow-y-auto outline-none">
    </div>
    <dialog open
      class="fixed z-100 top-1/3 w-full sm:max-w-sm sm:mx-auto mx-auto rounded-md border-none shadow-md p-0 m-0 overflow-x-auto flex flex-col justify-between">
      <header class="bg-sky-900 text-white w-auto p-3">
        <slot name="header">
          <h2 class="text-2xl font-semibold pl-2">{{ title }}</h2>
        </slot>
      </header>
      <section class="p-5">
        <slot></slot>
      </section>
      <!-- <div class="pb-4 pr-4 flex justify-end">
        <button @click="$emit('close')"
          class="p-2 px-3 border border-transparent shadow-sm text-lg font-medium rounded-md text-white bg-sky-900 hover:bg-cyan-800 focus:outline-none focus:ring-2 focus:ring-offset-2 ">Ok</button>
      </div> -->
    </dialog>
  </teleport>
</template>

<script>
export default {
  props: {
    title: {
      type: String,
      required: false,
    },
  },
  emits: ['close'],
};
</script>

<style scoped>
/* @media (min-width: 768px) {
  dialog {
    left: calc(50% - 20rem);

  }
} */
</style>