<template>
  <Market/>
</template>

<script>
import Market from "./components/Market.vue";
export default {
  name: "App",
  components: {
    Market: Market,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #2c3e50;
  margin: 0;
  height: 100%;
display: flex;
flex-direction: column;
}
html {
  margin: 0;
  height: 100%;
  background: rgba(235, 235, 235, 0.8);
  width: 100%;
}
body {
  margin: 0;
  height: 100%;
    width: 100%;
    overflow: hidden;
}
</style>
