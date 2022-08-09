<template>

  <section id="hero">
    <!-- FLEX CONTAINER -->
    <div class="container flex flex-col-reverse items-center px-6 mx-auto mt-10 space-y-0 md:space-y-0 lg:flex-row">
      <!-- LEFT FORM -->
      <div class="flex flex-col mb-32 space-y-1 lg:w-2/3">
        <h1 class="max-w-md text-4xl font-bold text-center md:text-5xl md:text-left pt-20">
          Ontdek jouw deal
        </h1>
        <p class="max-w-sm text-center text-slate-300 sm:text-slate-600 md:text-left pb-2">
          In minder dan een minuut
        </p>
        <!-- FORM 1 -->
        <div class="flex justify-center md:justify-start w-fit">
          <FormOne />
        </div>
        <!-- FORM 2 -->
        <div class="flex justify-center">
          <FormTwo />
        </div>
      </div>
      <!-- RIGHT IMAGE -->
      <div class="sm:w-auto w-1/2 mx-auto flex flex-shrink justify-end pl-30 md:justify-end">
        <img :src="dezelfde" alt="Dezelfde energie gewoon goedkoper" />
      </div>
    </div>
  </section>



  <!-- //form two
  //form three
  //form five
  //form six -->
</template>


<script>
import dezelfde from '../assets/Dezelfde-Energie.svg';
import FormOne from "../components/become-form/FormOne.vue";
import FormTwo from '@/components/become-form/FormTwo.vue';

export default {
  components: {
    FormOne,
    FormTwo
  },
  data() {
    return {
      dezelfde: dezelfde,
    }
  },
  methods: {

  }
}
</script>

<style>
</style>