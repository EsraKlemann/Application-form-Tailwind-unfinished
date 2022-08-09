<template>
  <FirstModal v-if="modalVisible" title="Woon/werkadres" @close="hideModal">
    <template #default>
      <p class="font-medium">Als een adres bedoeld is om te wonen of werken, heeft het een verblijfsfunctie
        en betaal je een lagere energiebelasting.
        Een adres zonder verblijfsfunctie is bijvoorbeeld een garagebox of volkstuin. </p>
    </template>
    <template #actions>
      <button @click="hideModal">Okay</button>
    </template>
  </FirstModal>

  <div class="mt-10 sm:mt-0">
    <!-- GRID -->
    <div class="md:grid md:grid-cols-3 md:gap-6">

      <div class="mt-5 md:mt-0 md:col-span-3">
        <form @submit.prevent="submitForm">
          <!-- BACKGROUND AND SHADOW BOX -->
          <div class="overflow-hidden sm:rounded-md">
            <!-- WHITE BOX -->
            <div class="px-4 py-5 bg-white sm:p-4 rounded-t-md">
              <!-- GRID -->
              <div class="grid grid-cols-6 gap-5 gap-y-4">

                <!-- POSTAL CODE -->
                <div :class="{ 'invalid': !postalCode.isValid }" class="col-span-6 sm:col-span-6">
                  <label for="postal"
                    class="block p-1 text-lg font-semibold text-gray-800 invalid:text-red-600">Postcode</label>
                  <input type="text" v-model.trim="postalCode.val" @blur="clearValidity('postalCode')" name="postal"
                    id="postal" autocomplete="postal-code" placeholder="1234AB"
                    :class="{ invalid: !postalCode.isValid }"
                    class=" placeholder:text-slate-200 block w-full rounded-md py-2 pl-2 pr-3 shadow-md focus:outline-none focus:ring-amber-400 invalid:ring-red-400/60 invalid:bg-red-400/60 invalid:border-red-400/60 focus:ring-2 sm:text-lg" />
                  <p v-if="!postalCode.isValid" class="text-red-700 block">De ingevulde postcode is niet juist</p>
                </div>

                <!-- NUMBER -->
                <div :class="{ invalid: !houseNumber.isValid }" class="col-span-6 sm:col-span-3">
                  <label for="housenr" class="block p-1 text-lg font-semibold text-gray-700">Huisnummer</label>
                  <input type="number" v-model.number="houseNumber.val" @blur="clearValidity('houseNumber')"
                    name="housenr" id="housenr" placeholder="123"
                    class=" placeholder:text-slate-200 block bg-white w-full rounded-md py-2 pl-2 pr-3 shadow-md focus:outline-none focus:border-orange-400 focus:ring-amber-400 focus:ring-2 sm:text-lg" />
                  <p v-if="!houseNumber.isValid" class="text-red-700 block">Dit is geen juist huisnummer</p>
                </div>

                <!-- ADDITION -->

                <div class="col-span-6 sm:col-span-3">
                  <!-- <button type="button" class="bg-white ..." disabled>
                    <svg class="animate-spin h-5 w-5 mr-3 ..." viewBox="0 0 24 24">
                      ... 
                     </svg>
                  </button> -->
                  <div v-if="isLoading">
                    <BaseSpinner />
                  </div>
                  <!-- has to become a dropdown i think -->
                  <!-- when !isloading and .... values in search are more than 1? -->
                  <div v-if="!isLoading">
                    <label for="addition"
                      class="sm:block p-1 text-lg font-semibold text-gray-700 invalid:text-red-600 ">Toevoeging</label>
                    <input type="text" v-model.trim="addition.val" name="addition" id="addition" placeholder="A"
                      class=" placeholder:text-slate-200 block bg-white w-full rounded-md py-2 pl-2 pr-3 shadow-md focus:outline-none focus:border-orange-400 focus:ring-amber-400  focus:ring-2 sm:text-lg" />
                  </div>
                </div>

                <div class="col-span-6">
                  <!-- TOGGLE -->
                  <div class="flex items-center justify-center w-full mb-4">
                    <!-- <p>{{verblijfsfunctie}}</p> -->
                    <label for="verblijfsfunctie" class="flex items-center cursor-pointer">
                      <!-- toggle -->
                      <div class="relative">
                        <!-- input -->
                        <input type="checkbox" v-model="verblijfsfunctie" name="verblijfsfunctie" id="verblijfsfunctie"
                          class="sr-only checked" @click="toggleVerblijfsfunctie">
                        <!-- line -->
                        <div class="line block bg-slate-200 w-14 h-8 rounded-full"></div>
                        <!-- dot -->
                        <div class="dot absolute right-1 top-1 bg-slate-50 w-6 h-6 rounded-full transition"></div>
                      </div>
                      <!-- label -->
                      <div class="ml-2 text-slate-400 font-medium sm:text-base">
                        Op dit adres kun je wonen of werken
                      </div>

                      <div>
                        <img :src="question" @click="showModal" @mouseenter="showModal" @mouseleave="hideModal"
                          class="w-5 ml-4 mr-3" />
                      </div>

                    </label>
                  </div>
                </div>
              </div>
            </div>
            <!-- GREY BOX AROUND BUTTON -->
            <div class="p-4 lg:pb-5 bg-gray-50">
              <p v-if="!formIsValid" class="p-2 text-red-700">Vul eerst de gegevens juist in</p>
              <NextButton />
            </div>

          </div>
        </form>
      </div>
    </div>
  </div>

</template>

<script>
import question from '@/assets/question.jpg'
import dezelfde from '@/assets/Dezelfde-Energie.svg'

import NextButton from '../ui/NextButton.vue'
import FirstModal from '@/components/modal/FirstModal.vue'
import BaseSpinner from '../ui/BaseSpinner.vue'

export default {
  components: { NextButton, FirstModal, BaseSpinner },
  emits: ['close'],
  data() {
    return {
      question: question,
      dezelfde: dezelfde,
      modalVisible: false,
      isLoading: false,

      postalCode: {
        val: '',
        isValid: true,
      },
      houseNumber: {
        val: null,
        isValid: true,
      },
      addition: {
        val: '',
        isValid: true,
      },
      verblijfsfunctie: true,

      formIsValid: true,
      error: null
    };
  },
  // computed: {
  //   compNumberPostal() {
  //     console.log('Checking number and postal code...');
  //     if (this.postalCode && this.houseNumber) {
  //       return this.
  //     }
  //   },
  // },
  watch: {
    // maybe these needed, only when i put these in the .val versions started working.
    // maybe also more logical to use this because we have access to value.isValid...?
    // postalCode: {
    //   handler(value) {
    //     if (value.val.length > 5) {
    //       console.log('checking postal')
    //     }
    //   },
    //   deep: true
    // },
    // houseNumber: {
    //   handler(value) {
    //     if (value.val.length > 0) {
    //       console.log('checking housenr')
    //     }
    //   },
    //   deep: true
    // },
    'postalCode.val'(post) {
      if (post.length > 5) {
        console.log('postal being checked');
        // set a value to true > computed with the value from number?
      }
    },
    'houseNumber.val'(number) {
      if (number > 0) {
        console.log('housenumber check')
      }
    },
    // postalCode(post) {
    //   if (post.val.length > 5) {
    //     console.log('postal and housenr are being checked')
    //     // this.getAddition;
    //   }
    // },

    // houseNumber() {
    //   if (this.houseNumber && this.postalCode) {
    //     console.log('housenr and postal are being checked')
    //     // this.getAddition;
    //   }
    // },
  },
  methods: {
    async searchRequest() {
      try {
        const res = await fetch('https://mega-become-test-default-rtdb.europe-west1.firebasedatabase.app/search.json')
        const responseData = await res.json();

        if (res.ok) {
          console.log(responseData)
        }
        if (!res.ok) {
          const error = new Error(responseData.message || 'Failed to fetch!');
          throw error;
        }
        this.availableAdditions = (await res.json())
        console.log(this.availableAdditions.toString)
      } catch (error) {
        console.log('Could not reach the API' + error)
      }
    },
    async getAddition() {
      // make spinner appear?
      // send search request
      this.isLoading = true;
      try {
        await this.searchRequest;
      } catch (error) {
        this.error = error.message || 'Something went wrong'
      }
      this.isLoading = false;
      // if ok, make spinner disappear
      // if not ok, red text. staat uw waarde hier niet tussen, neem contact op?
      // if ok read values and make dropdown appear. 
    },
    toggleVerblijfsfunctie() {
      this.verblijfsfunctie = !this.verblijfsfunctie
    },
    showModal() {
      this.modalVisible = true;
    },
    hideModal() {
      this.modalVisible = false;
    },
    clearValidity(input) {
      this[input].isValid = true;
    },
    validateForm() {
      this.formIsValid = true;

      if (this.postalCode.val === '' || this.postalCode.val.length != 6) {
        this.postalCode.isValid = false;
        this.formIsValid = false;
      }
      if (!this.houseNumber.val || this.houseNumber.val < 0) {
        this.houseNumber.isValid = false;
        this.formIsValid = false;
      }
    },
    submitForm() {
      this.validateForm();
      if (!this.formIsValid) {
        return;
      }

      const formData = {
        postal: this.postalCode.val.replace(/\s+/g, '').toUpperCase(),
        number: this.houseNumber.val,
        addition: this.addition.val,
        verblijfsfunctie: this.verblijfsfunctie

      }

      console.log(formData);

      fetch('https://mega-become-test-default-rtdb.europe-west1.firebasedatabase.app/step-one.json', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify(
          formData
        ),
      })
        .then((response) => {
          if (response.ok) {
            // ga naar volgende form stap. router beweeg naar invisible item? 
          } else {
            throw new Error('Could not save data!');
          }
        })
        .catch((error) => {
          console.log(error);
          this.error = error.message;
        });
    }
  },

}
</script>

<style>
/* Slider styles */
input:checked~.dot {
  transform: translateX(-100%);
  background-color: #ffffff;
}

input:checked~.line {
  background-color: #0c4a6e;
}
</style>