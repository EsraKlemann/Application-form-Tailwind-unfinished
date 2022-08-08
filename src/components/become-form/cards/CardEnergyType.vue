<template>

  <!-- WHITE OUTSIDE BORDER -->
  <div class="flex sm:flex-col items-center p-1 space-y-6 rounded md:w-1/3 overflow-hidden shadow-lg bg-white">
    <!-- IMAGE -->
    <img :src="require(`@/assets/energy-icons/${title}.png`)" class="w-20 sm:w-40 p-3" alt="image of energy type">
    <!-- TITLE TEXT -->
    <div class="px-6 h-20 text-center">
      <div class="font-bold sm:text-2xl mb-2 ">{{ title }}</div>
    </div>
    <!-- BUTTON TO CONTINUE -->
    <!-- <div class=" pt-4 pb-2">
      <span class="inline-block bg-gray-100 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-2">
        -></span>
    </div> -->
  </div>


</template>

<script>

export default {
  props: {
    title: {
      type: String,
      required: true
    },
    selected: {
      type: String,
      required: false
    }
  },
  data() {
    return {

    }
  },
  methods: {

  }
}
</script>