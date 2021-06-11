<template>
  <div id="app">
    <Slots />
  </div>
</template>

<script>
import Slots from "./components/Slots.vue";

export default {
  name: "App",
  components: {
    Slots,
  },
};
</script>

<style>
@font-face {
  font-family: "LCDDot Regular";
  font-style: normal;
  font-weight: normal;
  src: url("./assets/font/lcddot.woff2") format("woff2");
}

#app {
  font-family: "LCDDot Regular";
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  background: black;
  padding: 30px;
}

button {
  padding-top: 20px;
  padding-bottom: 20px;
  text-align: center;
  color: #000;
  text-transform: uppercase;
  font-weight: 600;
  margin-left: auto;
  margin-right: auto;
  margin-bottom: 10px;
  cursor: pointer;
  border-radius: 0px;
  -webkit-transition: all 0.15s ease-in-out;
  transition: all 0.15s ease-in-out;
  color: #00d7c3;
  border: 0px solid #00d7c3;
  background-color: transparent;
}

button:hover:not(:disabled) {
  box-shadow: 0 0 10px 0 #00d7c3 inset, 0 0 20px 2px #00d7c3;
}

button:disabled {
  color: #274147;
  cursor: not-allowed;
}
</style>
