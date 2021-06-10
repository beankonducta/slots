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
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

button {
  width: 170px;
  padding-top: 30px;
  padding-bottom: 30px;
  text-align: center;
  color: #000;
  text-transform: uppercase;
  font-weight: 600;
  margin-left: 30px;
  margin-bottom: 30px;
  cursor: pointer;
  background-color: transparent;
  border: 3px solid #00d7c3;
  border-radius: 0px;
  -webkit-transition: all 0.15s ease-in-out;
  transition: all 0.15s ease-in-out;
  color: #00d7c3;
}

button:hover:not(:disabled) {
  box-shadow: 0 0 10px 0 #00d7c3 inset, 0 0 20px 2px #00d7c3;
  border: 3px solid #00d7c3;
}

button:disabled {
  border: 3px dashed #a5e6f7;
  color: #a5e6f7;
  cursor: not-allowed;
}

.lcd {
  border-radius: 5px;
  padding: 10px;
  font-size: 1.5em;
  text-transform: uppercase;
  border: 1px solid orange;
  outline: none;
  background: white;
  max-width: 300px;
  margin: 0 auto;
}

.lcd:hover {
  cursor: pointer;
  background: #f3f3f3;
}

.lcd:active {
  background: #fcf3f3;
}

.lcd:disabled {
  cursor: not-allowed;
  background: white;
}
</style>
