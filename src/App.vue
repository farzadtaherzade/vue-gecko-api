<template>
  <Crypto />
</template>

<script>
import Crypto from "./components/Crypto.vue";

export default {
  name: "App",
  components: {
    Crypto,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #fff;
  display: flex;
  /* justify-content: center; */
  height:100vh;
  display: flex;
  justify-content: center;
}

*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body{
  background-color: #121212;
}
</style>
