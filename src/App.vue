<template>
  <NavBar />
  <router-view />
</template>

<script>
import NavBar from "./components/nav/NavBar.vue";

export default {
  components: {
    NavBar
  },
  data() {
    return {
    }
  },

}
</script>

<style>
#app {
  font-family: SpaceGrotesk;
  background-image: url("./assets/background/background-windturbine-gradient.jpg");
  background-repeat: no-repeat;
  background-size: 70rem;
  background-position: top right;
}
@media (max-width: 2000px) {
  #app { 
    background-size: 53rem;
  }
}

/* @media (max-width: 15px) {
  #app { 
    background-size: 60rem;
  }
} */

@media (max-width: 1440px) {
  #app { 
    background-size: 100%;
  }
}
@media (max-width: 976px) {
  #app {
    background-image: url("./assets/background/background-windturbine-horizontal-gradient.jpg");
    background-repeat: no-repeat;
    background-size: 61rem;
  }
}
</style>
