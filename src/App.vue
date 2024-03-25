<template>
  <Overview />
</template>

<script>
import Overview from "./components/SmartCalc.vue";

export default {
  name: "App",
  mounted() {
    document.title = "Example";
  },
  components: {
    Overview,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
