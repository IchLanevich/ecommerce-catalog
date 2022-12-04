<template>
  <div id="app">
    <ProductDisplay />
  </div>
</template>

<script>
import ProductDisplay from "./components/ProductDisplay.vue";

export default {
  name: "App",
  components: {
    ProductDisplay,
  },
  props: [],

  // setup() {
  //   onMounted(async () => {
  //     const response = await fetch("https://fakestoreapi.com/products/1");
  //     const res = await response.json();
  //     console.log(res)
  //   })
  // }
};
</script>

<style>
*,
::after,
::before {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
  color: #2c3e50;
  height: 100vh;
}
</style>
