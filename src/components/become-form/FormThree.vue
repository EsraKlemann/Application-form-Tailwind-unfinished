<template>
  <div></div>
</template>

<script>
export default {
  data() {
    return {

    }
  },
  created() {
    this.loadProducts();

  },
  methods: {
    submitForm() {
      fetch()
    },
    async loadProducts() {
      const response = await fetch('https://mega-become-test-default-rtdb.europe-west1.firebasedatabase.app/products',
      );
      const responseData = await response.json();

      if (!response.ok) {
        //error handling
      }

      const products = [];

      for (const key in responseData) {
        const product = {
          code: responseData[key].code,
          energy_type: responseData[key].energy_type,
          contract_type: responseData[key].contract_type,
          duration: responseData[key].duration,
          id: responseData[key].id,
          descriptions: responseData[key].descriptions,
        }
        products.push(product);
      }

    }
  }
}

</script>



