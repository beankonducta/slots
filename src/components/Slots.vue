<template>
  <div class="slots">
    <div class="reels">
      <Reel ref="reelOne" :speed="25" @spun="spun(0, $event)" />
      <Reel ref="reelTwo" :speed="16" @spun="spun(1, $event)" />
      <Reel ref="reelThree" :speed="12" @spun="spun(2, $event)" />
    </div>
    <div class="spacer"></div>
    bal: {{ balance }} pay: {{ payout }}
    <br />
    <button @click="roll()" :disabled="active">Roll</button>
    <br />
    <br />
    lines: {{ multiplier }}
    <br />
    <button @click="multChange(-1)" :disabled="active">-</button>
    <button @click="multChange(1)" :disabled="active">+</button>
    <br />
    <br />
    bet: {{ bet }}
    <br />
    <button @click="betChange(-10)" :disabled="active">-</button>
    <button @click="betChange(10)" :disabled="active">+</button>
  </div>
</template>

<script>
import Reel from "./Reel.vue";

export default {
  name: "Slots",
  components: {
    Reel,
  },
  props: {},
  data() {
    return {
      balance: 1000,
      bet: 10,
      multiplier: 1,
      payout: 0,
      reels: [
        { spun: false, values: [0, 0, 0] },
        { spun: false, values: [0, 0, 0] },
        { spun: false, values: [0, 0, 0] },
      ],
      active: false,
    };
  },
  methods: {
    roll() {
      this.active = true;
      this.payout = 0;
      this.removeBet();
      this.$refs.reelOne.spin(300, 300);
      this.$refs.reelTwo.spin(300, 300);
      this.$refs.reelThree.spin(300, 300);
    },
    multChange(val) {
      if (val === 1 && this.multiplier < 3) this.multiplier += val;
      else if (val === -1 && this.multiplier > 1) this.multiplier += val;
    },
    betChange(val) {
      if (val === 10 && this.bet < 100) this.bet += val;
      else if (val === -10 && this.bet > 10) this.bet += val;
    },
    removeBet() {
      this.balance -= this.bet * this.multiplier;
    },
    spun(reel, value) {
      this.reels[reel].spun = true;
      this.reels[reel].values = value;
      for (let reel of this.reels) if (!reel.spun) return;
      this.active = false;
      this.payoutWinnings();
    },
    // TODO: Refactor
    payoutWinnings() {
      this.reels.forEach((val) => (val.spun = false));
      let payout = 0;
      for (let i = 0; i < this.reels.length - 1; i++)
        if (
          this.reels[0].values[i] === this.reels[1].values[i] &&
          this.reels[1].values[i] === this.reels[2].values[i]
        )
          if (i === 0 || this.multiplier > 1)
            payout += this.bet * this.multiplier * this.reels[0].values[i];
      if (
        this.reels[0].values[0] === this.reels[1].values[1] &&
        this.reels[1].values[1] === this.reels[2].values[2] &&
        this.multiplier >= 3
      )
        payout += this.bet * this.multiplier * this.reels[0].values[0];
      if (
        this.reels[0].values[2] === this.reels[1].values[1] &&
        this.reels[1].values[1] === this.reels[2].values[0] &&
        this.multiplier >= 3
      )
        payout += this.bet * this.multiplier * this.reels[0].values[2];
      this.payout = payout;
      this.balance += this.payout;
    },
  },
  computed: {
    canRoll() {
      return this.balance >= this.bet * this.multiplier;
    },
  },
};
</script>
<style scoped>
.slots {
  width: 100%;
}
.reels {
  width: 25%;
  display: flex;
  flex-direction: row;
  margin: 0 auto;
}
.spacer {
  height: 200px;
}
</style>
