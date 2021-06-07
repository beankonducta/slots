<template>
  <div class="reel">
    <div class="small-value">
      {{ valAt(-1) }}
    </div>
    <div class="value">
      {{ values[valueSlot] }}
    </div>
    <div class="small-value">
      {{ valAt(1) }}
    </div>
  </div>
</template>

<script>
export default {
  name: "Reel",
  props: {},
  data() {
    return {
      values: [
        // 1, 1, 1, 1, 1, 1, 1.25, 1.25, 1.25, 1.25, 1.5, 1.5, 1.5, 1.75, 1.75,
        // 1.75, 2, 2, 2, 2.5, 2.5, 3, 3, 3.5, 3.5, 5, 10, 15,
        1, 2, 3, 4, 5, 6, 7, 8, 9, 10,
      ],
      valueSlot: 0,
      speed: 10,
    };
  },
  methods: {
    spin(spins, initial) {
      setTimeout(() => {
        spins--;
        if (this.valueSlot < this.values.length - 1) this.valueSlot++;
        if (this.valueSlot === this.values.length - 1) this.valueSlot = 0;
        if (spins > Math.floor(Math.random() * 100)) this.spin(spins, initial);
      }, (initial - spins) / this.speed);
    },
    valAt(relativeSlot) {
      if (this.valueSlot + relativeSlot < 0)
        return this.values[
          this.values.length - 1 + this.valueSlot + relativeSlot
        ];
      if (this.valueSlot + relativeSlot > this.values.length - 1)
        return this.values[
          this.valueSlot + relativeSlot - this.values.length - 1
        ];
      return this.values[this.valueSlot + relativeSlot];
    },
  },
};
</script>

<style scoped>
.reel {
  width: 100%;
  text-align: center;
}
.value {
  font-size: 2em;
}
.value-small {
  font-size: 1em;
}
</style>
