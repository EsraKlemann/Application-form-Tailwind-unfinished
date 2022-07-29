<template>
  <div class="px-4 py-5 sm:p-4 rounded-md bg-gray-100 flex row-auto p-2 space-x-3">
    <CardEnergyType @click="gasSelection" :class="{ 'bg-sky-800': selected === 'Gas' }" title="Gas"></CardEnergyType>
    <CardEnergyType @click="electraGasSelection" :class="{ 'bg-sky-800': selected === 'Stroom & Gas' }" title="Stroom & Gas"></CardEnergyType>
    <CardEnergyType @click="electraSelection"  :class="{ 'bg-sky-800': selected === 'Stroom' }" title="Stroom"></CardEnergyType>   
  </div>
</template>

<script>
import CardEnergyType from './cards/CardEnergyType.vue'
export default {
  components: {
    CardEnergyType
  },
  data() {
    return {
      selected: '',
    }
  },
  methods: {
    electraSelection() {
      this.selected = 'Stroom'
    },
    electraGasSelection() {
      this.selected = 'Stroom & Gas'
    },
    gasSelection() {
      this.selected = 'Gas'
    }
  }
}

</script>