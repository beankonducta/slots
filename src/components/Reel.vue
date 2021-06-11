<template>
  <div class="reel">
    <div class="value-container">
      <img class="value-small" :src="imgAt(-1)" :key="valueSlot - 1" />
    </div>
    <div class="value-container">
      <img class="value" :src="imgAt(0)" :key="valueSlot" />
    </div>
    <div class="value-container">
      <img class="value-small" :src="imgAt(1)" :key="valueSlot + 1" />
    </div>
  </div>
</template>

<script>
export default {
  name: "Reel",
  props: {
    speed: Number,
  },
  data() {
    return {
      values: [
        1, 1, 1, 1, 1, 1, 2, 2, 2, 2, 2, 2, 3, 3, 3, 1, 1, 1, 1, 1, 1, 4, 4, 4,
        5, 5, 5, 6, 6, 6, 10, 10, 1, 1, 1, 1, 1, 1, 15, 15, 20, 30, 50, 2, 2, 2,
        3, 3, 3,
      ],
      valueSlot: 0,
    };
  },
  methods: {
    spin(spins, initial) {
      // i should weight this so the wheels spin and very slightly different speeds
      setTimeout(() => {
        spins--;
        if (this.valueSlot < this.values.length - 1) this.valueSlot++;
        if (this.valueSlot === this.values.length - 1) this.valueSlot = 0;
        if (spins > Math.floor(Math.random() * 5)) this.spin(spins, initial);
        else this.$emit("spun", this.valuesArray);
      }, (initial - spins) / this.speed);
    },
    valAt(relativeSlot) {
      if (this.valueSlot + relativeSlot < 0)
        return this.values[this.values.length + this.valueSlot + relativeSlot];
      if (this.valueSlot + relativeSlot > this.values.length)
        return this.values[this.valueSlot + relativeSlot - this.values.length];
      return this.values[this.valueSlot + relativeSlot];
    },
    imgAt(relativeSlot) {
      return require(`@/assets/fruit/f${this.valAt(relativeSlot)}.png`);
    },
  },
  computed: {
    valuesArray() {
      return [this.valAt(-1), this.values[this.valueSlot], this.valAt(1)];
    },
  },
};
</script>

<style scoped>
.reel {
  width: 100%;
  height: 80%;
  border: 0.5px solid black;
  background: #685992;
}
.value-container {
  width: 120px;
  margin: 0 auto;
}
.value {
  font-size: 2em;
  height: 100px;
}
.value-small {
  font-size: 1em;
  height: 50px;
}
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
</style>
