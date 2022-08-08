<template>
  <!-- CONTAINER HEADING AND ENERGY BLOCKS -->
  <div class="max-w-7xl px-5 mx-auto mt-32 text-center">
    <!-- HEADING -->
    <h2 class="text-3xl font-bold text-center">
      Kies uw energie
    </h2>
    <!-- CONTAINER CARDS -->
    <div class="flex flex-col bg-slate-50 mt-3 px-2 sm:flex-row sm:space-x-2 ">
      <!-- ENERGY CARDS -->
      <CardEnergyType @click="gasSelection" title="Gas"
        :class="{ 'bg-sky-800 transition ease-in-out translate-y-0 duration-200': selected === 'Gas' }" />
      <CardEnergyType @click="electraGasSelection" title="Stroom & Gas"
        :class="{ 'bg-sky-800': selected === 'Stroom & Gas' }" />
      <CardEnergyType @click="electraSelection" title="Stroom" :class="{ 'bg-sky-800': selected === 'Stroom' }" />
    </div>
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
      gasFormVisible: false,

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
    },
    async getContract() {
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
          name: responseData[key].code,
          contractType: responseData[key].contract_type,
          duration: responseData[key].duration,
          energyType: responseData[key].energy_type,
          id: key,
          descriptions: responseData[key].descriptions,
        }
        contracts.push(contract);
      }
    }
  }
}

</script>