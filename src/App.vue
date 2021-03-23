<template>
  <div id="app">
    <Item />
    <Features />
  </div>

</template>

<script>
import "bootstrap/dist/css/bootstrap.css";
import "font-awesome/css/font-awesome.css";
import Item from "./components/Item";
import Features from "./components/Features";
export default {
  name: "App",
  components: {
    Item,
    Features
  }

}
</script>

<style>
body {
  background: #f0f3f5;
  color: #81929b;
}


#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin-top: 20px;
}
</style>
