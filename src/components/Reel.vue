<template>
  <div class="reel">
    <div class="value-container" v-for="(value, index) in values" :key="index">
      <img class="value" :class="winClass(index)" :src="img(index)" />
    </div>
  </div>
</template>

<script>
export default {
  name: "Reel",
  props: {
    speed: Number,
    winner: Array,
  },
  data() {
    return {
      values: [
        1, 1, 1, 1, 1, 1, 2, 2, 2, 2, 2, 2, 3, 3, 3, 1, 1, 1, 1, 1, 1, 4, 4, 4,
        5, 5, 5, 6, 6, 6, 10, 10, 1, 1, 1, 1, 1, 1, 15, 15, 20, 30, 50, 2, 2, 2,
        3, 3, 3,
      ],
    };
  },
  methods: {
    winClass(index) {
      for (let win of this.winner) if (win === index) return "winner";
      return "standard";
    },
    spin(spins, initial) {
      setTimeout(() => {
        spins--;
        this.values.unshift(this.values.pop());
        if (spins > Math.floor(Math.random() * 5)) this.spin(spins, initial);
        else {
          this.$emit("spun", this.values);
        }
      }, (initial - spins) / this.speed);
    },
    img(index) {
      return require(`@/assets/fruit/f${this.values[index]}.png`);
    },
  },
  computed: {},
};
</script>

<style scoped>
.reel {
  width: 100%;
  height: 80%;
  border: 0.5px solid black;
  background: rgb(0, 0, 0);
  background: linear-gradient(
    0deg,
    rgba(0, 0, 0, 1) 0%,
    rgba(28, 5, 40, 1) 50%,
    rgba(0, 0, 0, 1) 100%
  );
  display: flex;
  flex-direction: column;
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
  -webkit-animation: slide-bottom 0.5s cubic-bezier(0.25, 0.46, 0.45, 0.94) both;
  animation: slide-bottom 0.5s cubic-bezier(0.25, 0.46, 0.45, 0.94) both;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}

img {
}

.standard {
}

.winner {
  filter: invert(60%) sepia(89%) saturate(5014%) hue-rotate(165deg)
    brightness(101%) contrast(102%);
}

@-webkit-keyframes slide-bottom {
  0% {
    -webkit-transform: translateY(0);
    transform: translateY(0);
  }
  100% {
    -webkit-transform: translateY(100px);
    transform: translateY(100px);
  }
}
@keyframes slide-bottom {
  0% {
    -webkit-transform: translateY(0);
    transform: translateY(0);
  }
  100% {
    -webkit-transform: translateY(100px);
    transform: translateY(100px);
  }
}
</style>
