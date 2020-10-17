<template>
  <div id="app">
    <NavBar />
    <div class="container">
      <div class="page-text__div my-5">
        <h1 class="mb-3">Vermicompost Calculator</h1>
        <p class="mt-4">
          Just simply enter the dimensions of you garden bed and find out how
          much vermicompost you'd need to for beneficial effects.
        </p>
      </div>

      <Calculator />
    </div>
  </div>
</template>

<script>
import NavBar from "./components/NavBar.vue";
import Calculator from "./components/Calculator.vue";

export default {
  name: "App",
  components: {
    NavBar,
    Calculator,
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
}
</style>
