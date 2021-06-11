<template>
  <div class="lcd">
    <div class="title">{{ title }}</div>
    <div class="value">{{ formattedValue }}</div>
  </div>
</template>

<script>
export default {
  name: "Lcd",
  props: {
    title: String,
    value: [],
    type: String,
  },
  data() {
    return {};
  },
  methods: {},
  computed: {
    formattedValue() {
      if (this.type === "MONEY") return "$" + this.value;
      return this.value;
    },
  },
};
</script>

<style scoped>
.lcd {
  font-family: "LCDDot Regular";
  width: 100%;
  height: 80px;
  color: #000;
  text-transform: uppercase;
  font-weight: 600;
  background-color: #0a0000;
  border: 3px solid #411f1f;
  border-radius: 0px;
  -webkit-transition: all 0.15s ease-in-out;
  transition: all 0.15s ease-in-out;
}

.title {
  float: left;
  margin-top: 10px;
  margin-left: 10px;
  color: #7c1b1b;
  font-size: 0.75em;
}

.value {
  color: red;
  margin: 0 auto;
  margin-top: 30px;
  font-size: 2em;
}

.lcd:disabled {
  cursor: not-allowed;
  background: black;
  color: #200505;
}
</style>
