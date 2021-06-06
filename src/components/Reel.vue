<template>
  <div class="reel">
    <div class="value">
      {{ values[valueSlot] }}
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
        1, 1, 1, 1, 1, 1, 1.25, 1.25, 1.25, 1.25, 1.5, 1.5, 1.5, 1.75, 1.75,
        1.75, 2, 2, 2, 2.5, 2.5, 3, 3, 3.5, 3.5, 5, 10, 15,
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
  },
};
</script>

<style scoped>
.reel {
  width: 100%;
}
</style>
