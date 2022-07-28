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
  background-size: 49%;
  background-position: top right;
}

@media (max-width: 976px) {
  #app {
    background-image: url("./assets/background/background-windturbine-horizontal-gradient.jpg");
    background-repeat: no-repeat;
    background-size: 58rem;
  }
}
</style>
