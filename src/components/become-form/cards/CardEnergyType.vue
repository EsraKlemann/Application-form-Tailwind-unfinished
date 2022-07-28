<template>
  <div  class="max-w-md rounded overflow-hidden shadow-lg bg-white">
    <img :src="require(`@/assets/energy-icons/${title}.png`)" class="h-40" alt="test">
    <div class="px-6 py-4">
      <div class="font-bold text-xl mb-2">{{title}}</div>
    </div>
    <div class="px-6 pt-4 pb-2">
      
      <span
        class="inline-block bg-gray-100 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-2"
        >Bekijk prijzen -></span>
    </div>
  </div>
</template>

<script>

export default {
  props: {
    title: {
      type: String,
      required: true
    },
  },
  data() {
    return {
    }
  },
  methods: {
    getContract() {
      const response = await fetch('https://mega-become-test-default-rtdb.europe-west1.firebasedatabase.app/products.json');

      const responseData = await response.json();
      if (response.ok) {
        // ga naar volgende form stap. router beweeg naar invisible item? 
      } else {
        throw new Error('Could not save data!');
      }

      const contracts = [];

      for (const key in responseData) {
        const contract = {
          
        }

      }
    }
  }
}
</script>