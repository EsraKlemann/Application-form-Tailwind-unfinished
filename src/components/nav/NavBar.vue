<template>
  <header>
    <!-- Navbar -->
    <nav class="relative container mx-auto p-3">
      <!-- Flex container -->
      <div class="flex items-center justify-between">
        <!-- Logo -->
        <div class="pt-1">
          <router-link to="/">
            <h2
              class="p-2 font-extrabold text-transparent text-5xl bg-clip-text bg-gradient-to-br from-orange-400 to-yellow-400">
              Mega</h2>
          </router-link>
        </div>

        <!--menu items-->
        <div class="hidden text-xl text-gray-200 space-x-6 md:flex ">
          <router-link to="/" class=" hover:text-gray-500">Home</router-link>
          <router-link to="/become" class="hover:text-gray-500">Become</router-link>
        </div>


        <!--  Hamburger Menu Icon Mobile-->
        <button id="menu-btn" @click="changeVisibility" :class="{ open: hamburgerOpen }"
          class="block hamburger md:hidden focus:outline-none">
          <span class="hamburger-top"></span>
          <span class="hamburger-middle"></span>
          <span class="hamburger-bottom"></span>
        </button>
      </div>

      <!--mobile menu-->
      <div class="md:hidden">
        <div id="menu" :class="burgerMenuOpen"
          class="absolute flex-col items-center self-end py-8 mt-10 space-y-6 font-bold bg-white sm:w-auto sm:self-center left-6 right-6 drop-shadow-md">
          <router-link to="/">Home</router-link>
          <router-link to="/become" class="hover:text-gray-500">Become</router-link>
        </div>
      </div>
    </nav>
  </header>
</template>

<script>
export default {
  props: ['mode'],
  data() {
    return {
      hamburgerOpen: false,
    }
  },
  methods: {
    changeVisibility() {
      this.hamburgerOpen = !this.hamburgerOpen;
    },
  },
  computed: {
    burgerMenuOpen() {
      return this.hamburgerOpen === true ? 'flex' : 'hidden';
    }
  }




}


</script>

<style scoped>
/* Hamburger Menu */
.hamburger {
  cursor: pointer;
  width: 24px;
  height: 24px;
  transition: all 0.25s;
  position: relative;
}

.hamburger-top,
.hamburger-middle,
.hamburger-bottom {
  position: absolute;
  top: 0;
  left: 0;
  width: 24px;
  height: 2px;
  background: #000;
  transform: rotate(0);
  transition: all 0.5s;
}

.hamburger-middle {
  transform: translateY(7px);
}

.hamburger-bottom {
  transform: translateY(14px);
}

.open {
  transform: rotate(90deg);
  transform: translateY(0px);
}

.open .hamburger-top {
  transform: rotate(45deg) translateY(6px) translateX(6px);
}

.open .hamburger-middle {
  display: none;
}

.open .hamburger-bottom {
  transform: rotate(-45deg) translateY(6px) translateX(-6px);
}
</style>