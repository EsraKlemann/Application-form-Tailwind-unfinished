<template>
  <div class="bg-gray-100 flex row-auto">
    <CardEnergyType @click="electraSelection" title="Stroom" :class="{ 'bg-sky-800': selected === 'Stroom' }" ></CardEnergyType>
    <CardEnergyType @click="electraGasSelection" :class="{ 'bg-sky-800': selected === 'Stroom & Gas' }" title="Stroom & Gas"></CardEnergyType>
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
  }
}

</script>