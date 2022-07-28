<template>
  <div  class="max-w-sm rounded overflow-hidden shadow-lg">
    <img :src="require(`@/assets/energy-icons/${title}.png`)" class="w-full" alt="test">
    <div class="px-6 py-4">
      <div class="font-bold text-xl mb-2">{{title}}</div>
    </div>
    <div class="px-6 pt-4 pb-2">
      
      <span
        class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-2"
        >Bekijk prijzen -></span>
    </div>
  </div>
</template>

<script>
import Stroom from "@/assets/energy-icons/Stroom.png";
import StroomGas from "@/assets/energy-icons/Stroom & Gas.png"

export default {

  props: {
    title: {
      type: String,
      required: true
    },
    sourceImage: {
      type: String,
      required: true
    }
  },
  data() {
    return {
      StroomImage : Stroom,
      StroomGasImage: StroomGas
    }
  },
  methods: {
  }
}
</script>