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
  border-radius: 5px;
  padding: 10px;
  font-size: 1.5em;
  text-transform: uppercase;
  border: 1px solid orange;
  outline: none;
  background: white;
}

button:hover {
  cursor: pointer;
  background: #f3f3f3;
}

button:active {
  background: #fcf3f3;
}

button:disabled {
  cursor: not-allowed;
  background: white;
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
